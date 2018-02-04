# data-engineering-patterns

## Patterns

* ES Streams  
  https://streams.spec.whatwg.org/
  
* ES Observables  
  https://github.com/tc39/proposal-observable

* ES Iterators  
  http://exploringjs.com/es6/ch_iteration.html
 
  * http://exploringjs.com/es6/ch_iteration.html#sec_iterability
  
    * ```typescript
      interface Iterable {
          [Symbol.iterator]() : Iterator;
      }
      interface Iterator {
          next() : IteratorResult;
      }
      interface IteratorResult {
          value: any;
          done: boolean;
      }  
      ```

    * ![](http://exploringjs.com/es6/images/iteration----consumers_sources.jpg)  

    * > Data consumers: JavaScript has language constructs that consume data. For example, for-of loops over values and the spread operator (...) inserts values into Arrays or function calls.

      > ES6 introduces the interface Iterable. Data consumers use it, data sources implement it


* ES Async Iterators  
  https://github.com/tc39/proposal-async-iteration
  
  * http://2ality.com/2016/10/asynchronous-iteration.html
  
  * [Why Async Iterators Matter](https://docs.google.com/presentation/d/1r2V1sLG8JSSk8txiLh4wfTkom-BoOsk52FgPBy8o3RM/edit?usp=sharing)
  
    ![](https://pbs.twimg.com/media/DUyiW_8X0AAadXm.jpg:large)

* ES Callbags
  
  * [Why we need Callbags](https://staltz.com/why-we-need-callbags.html)


## Topics

### Streams vs Observables

* https://github.com/whatwg/streams/blob/master/FAQ.md  
  > Observables/EventTarget are specifically designed for multi-consumer scenarios, and have no support for backpressure.

  > Observables and readable streams both share the semantic of "zero or more chunks, followed by either an error or done signal". But beyond that, they are not very comparable.


### Streams vs Async Iterables

* https://github.com/whatwg/streams/blob/master/FAQ.md  
  > readable streams are a specialized type of async iterable optimized for things like off-main-thread data transfer and precise backpressure signaling


## To Read

* https://github.com/cyclejs/cyclejs/issues/581

* https://vimeo.com/album/4578937

* https://www.youtube.com/watch?v=sTSQlYX5DU0

* https://github.com/ReactiveX/rxjs/issues/752#issuecomment-161234549

* https://medium.com/@benlesh/learning-observable-by-building-observable-d5da57405d87

* https://github.com/tc39/proposal-observable/issues/43#issuecomment-121003367

* https://github.com/ReactiveX/rxjs/issues/29

* https://github.com/pull-stream/pull-stream
