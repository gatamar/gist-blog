# Reactive design

https://learning.oreilly.com/library/view/why-reactive/9781492048961

## Reactive Streams

Reactive Stream is just smth reactive, it marks the concept of generating data flow, and has source and destination. A destination has a "capacity per time", so if the source produces data faste than destination processes it, that's not very good. 
A "back pressure" concept means smth like "it's the stream's responsibility to handle async destination's nature" - as I understand it now, the Source can emit some data entity at _t1_, and Destination can receive that data at _t2_ on the other thread, because at _t1_ it's blocked/ doing some heavy op.
And it's Stream's responsibility to gurantee that.
Links: 
1. General overview: http://www.reactive-streams.org
2. Nice iOS thoughts which say that Combine = RxSwift + back-pressure mechanism, and that back-pressure is related to keeping a low RAM footprint: https://paulwoodiii.com/development-blog/2019/8/1/apples-combine-and-reactive-programming-with-back-pressure
3. iOS technical explanation, some custom (bycicle) implementation: https://tanaschita.com/20211205-back-pressure-in-combine/
4.

# Reactive implementations other than iOS

Akka, Erlang
