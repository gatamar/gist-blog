In the previous iteration of my pet project I've used `CoreData`. It sucks. The main reason is that it's not SQL-based, and I know SQL good enough to have a mental block when designing some kind of ER diagram.
In the current iteration I'm just adding features on top of `Readium` opensource code. So they wrote a simple SQLLite wrapper, and I'm using it as a dependency for my own framework.

Today I've added a possibility to delete entities instead of just inserting them. :) 
So there's such stuff as `Connection`, `Table`, `Expression`, `query: SQLLite.Insert`, `query: SQLLite.Delete`, `query: SQLLite.Update`. 
As nice and simple as Python's `sqlalchemy`. 

Waiting to do performance and threads optimizations if needed.
