So I developed a basic understanding of how to approach this stuff, but this understanding is vague, so I'm probally missing something, and I hate this feeling, because it happened so many times already.

Let's describe the problem roughly. There's a screen for doing mind maps. It has "blocks" and "connections". Maybe it has something else, but we assume this doesn't matter. Each block has a text, color, position on the screen, and so on. Each connection connects two blocks (so it's position is autocalculated), has a color, dash pattern and so on. We want to let the user to edit the mind map, persist that changes, and undo/redo some count of the last changes (let's assume the device memory is endless, so we persist all the changes).

Some prerequisites:
1. a relational db is used, so it's SQLite, or more specifically, GRDB.
2. Combine is used for API; at a high level it shouldn't matter, it's just much more convenient (which means I don't feel the other advantages of Reactive concepts for mobile other than convenience and a lower cognitive load)   

What I don't undestand (because I don't know the patterns):
1. there's such concept as a "unidirectional flow". The first thing which comes to mind for this reactive persistence API is that I update the [view]model each time the storage says something changes. But in this mind map case, it's a view[model] who asked the storage to persist the last changes, so after the storages updates smth, and pings the model back, the model at least doesn't need that, and at last it may be changed  again already by the user, so that callback from the persistence will update the stuff back.

My current assumption for doing this that if we use GRDB in this reactive model, we _read_ from it only when "opening" the mind map. We read in a background, all this time we show some loading indicator, then after we finished reading, we hide an indicator, _close the subscription_, and each time in this session we only write to the GRDB.
The question which must be anwered before coding this, is that will GRDB give us smth like "all this data I gave you via the subscription is up-to-date with the storage, so it's not an intermediate fetch result".


2. Which is better to store: the snapshots, or the incremental changes?
I guess it's a tradeoff which depends on multiple factors such as: data size, number of changes, speed of reading/writing/applying that changes.
But in general, I assume that having the list of changes is enough, so we don't need to save the snapshot on each new change persisted. And if because of some memory/performance/UX reasons we decide to have only N last history records, we'll calc the "first" shapshot, and leave the changes after it. This will be done without notifying the user, it's parametric and optional, such that the basic implementation should allow this tweak, but also it should work well without it.

Now, what's left is to define the API for the "block"/"connection"/"change"/"change-persistor"/"change-applier"/"change-deapplier".

The entities can look like this:
```
Block {
	id
	text
	color
	position
}

Connection {
	id
	id_block1
	id_block2
	color
}
```

And the changes for undo/redo can look like this:
```
BlockChangeUpdate {
	block_id
	(text_before, text_after)?
	(pos_before, pos_after)?
	(color_before, color_after)?
}

ConnectionChangeUpdate {
	connection_id
	(color_before, color_after)?
}
```
but these are only the update changes.

So for the creation/deletion we need some other struct. Swift `enums` should appear, and `decode`/`encode` implementation should be ensured.
I'll just remind to myself, that all is functional, it's immutable, all this "domain boundaries" should be kept. But I don't know how to do it in a systematic way, so let's just use "looks good"/"doesn't look good". 
A one pattern I've seen for this is an enum with associated values, each of them is a corresponding structure.
I don't remember the exact code for encode/decode, so should look it up until I can read that codebase :D.
The API will look like this:
```
BlockChangeUpdate //  see above

ConnectionChangeUpdate //  see above

BlockChangeCreateOrDelete {
	(block_before?, block_after?)
}

ConnectionChangeCreateOrDelete {
	(conn_before?, conn_after?)
}

enum ChangeTypes {
	case blockChangeUpdate(BlockChangeUpdate)
	case connectionChangeUpdate(ConnectionChangeUpdate)
	case blockChangeCreateOrDelete(BlockChangeCreateOrDelete)
	case connectionChangeCreateOrDelete(ConnectionChangeCreateOrDelete)
}

struct ChangeItself: Decodable {
	let parts: [ChangeTypes]
	func encode() // tough stuff, but I've seen a pattern
	func decode() // tough stuff, but I've seen a pattern

	func applyForward() // set "block_after?"
	func applyBackward() // set "block_before?"
}
```

Now, when the user deletes a block, all connections for this block are also deleted.
So the `ChangeItself` may be created like this:
```
ChangeItself(
	[
		.blockChangeCreateOrDelete(
			BlockChangeCreateOrDelete((4, nil))
		),
		.connectionChangeCreateOrDelete(
			ConnectionChangeCreateOrDelete((13, nil))
		),
		.connectionChangeCreateOrDelete(
			ConnectionChangeCreateOrDelete((15, nil))
		)
	]
)
```

Then, when the user pressed "undo", this `ChangeItself` is replayed, and Block #4, and Connections #13 and #15 are returned back to the [view]model. So when the user deletes some entity, we don't delete that entity from the db, we just create a corresponding change.

The ponential issue I can see is that when the user presses "undo", and then makes a new change, we have to delete that last previous change from the persistence. It's not hard, but in some cases some blocks/connections should also be deleted, if they were both created and deleted within the lifetime of that deleted subarray of changes.
But it's just an optimization, it shouldn't affect the basic implementation.

