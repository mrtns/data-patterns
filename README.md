# data-engineering-patterns

## Patterns

* ES Streams  
  https://streams.spec.whatwg.org/

* [Functional reactive programming](https://en.wikipedia.org/wiki/Functional_reactive_programming)

* Reactive extensions

  * ES Observables  
    https://github.com/tc39/proposal-observable
  
  * [Reactive extensions](https://en.wikipedia.org/wiki/Reactive_extensions)

* [Functional reactive programming](https://en.wikipedia.org/wiki/Functional_reactive_programming)

  * > Functional reactive programming (FRP) is a programming paradigm for reactive programming (asynchronous dataflow programming) using the building blocks of functional programming (e.g. map, reduce, filter).
  
    > aiming to simplify these problems by explicitly modeling time.

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
      
      > Iterable and iterators are part of a so-called protocol (interfaces plus rules for using them) for iteration. A key characteristic of this protocol is that it is sequential: the iterator returns values one at a time. That means that if an iterable data structure is non-linear (such as a tree), iteration will linearize it.


* ES Async Iterators  
  https://github.com/tc39/proposal-async-iteration
  
  * http://2ality.com/2016/10/asynchronous-iteration.html
  
  * [Why Async Iterators Matter](https://docs.google.com/presentation/d/1r2V1sLG8JSSk8txiLh4wfTkom-BoOsk52FgPBy8o3RM/edit?usp=sharing)
  
    ![](https://pbs.twimg.com/media/DUyiW_8X0AAadXm.jpg:large)

* ES Generators  
  http://exploringjs.com/es6/ch_generators.html  
  
  * [Implementing iterables via generators](http://exploringjs.com/es6/ch_generators.html#_implementing-iterables-via-generators)
  
    * [Iterable combinators (e.g. `take()`)](http://exploringjs.com/es6/ch_generators.html#_the-iterable-combinator-take)
      (Including [Infinite iterables](http://exploringjs.com/es6/ch_generators.html#_infinite-iterables-1))
  
  * [Generators for lazy evaluation](http://exploringjs.com/es6/ch_generators.html#_generators-for-lazy-evaluation)
    
    * [Generators as iterators (data production)](http://exploringjs.com/es6/ch_generators.html#_lazy-pull-generators-as-iterators)
      > Lazy pull with generators works as follows. The three generators implementing steps 1–3 are chained as follows:

      ```
      const CHARS = '2 apples and 5 oranges.';
      const CHAIN2 = addNumbers(extractNumbers(tokenize(logAndYield(CHARS))));
      [...CHAIN2];
      ```
      > Each of the chain members pulls data from a source and yields a sequence of items. Processing starts with tokenize whose source is the string CHARS.
      
      ```
      function* logAndYield(iterable, prefix='') {
        for (const item of iterable) {
          console.log(prefix + item);
          yield item;
        }
      }
      ```
      
    * [Generators as observers (data consumption)](http://exploringjs.com/es6/ch_generators.html#_lazy-push-generators-as-observables)
          
      ```
      const INPUT = '2 apples and 5 oranges.';
      const CHAIN = tokenize(extractNumbers(addNumbers(logItems())));
      send(INPUT, CHAIN);
      ```
      
      ```
      /**
       * Pushes the items of `iterable` into `sink`, a generator.
       * It uses the generator method `next()` to do so.
       */
      function send(iterable, sink) {
          for (const x of iterable) {
              sink.next(x);
          }
          sink.return(); // signal end of stream
      }      
      ```
    
    * [Generators as coroutines (cooperative multitasking)](http://exploringjs.com/es6/ch_generators.html#_cooperative-multi-tasking-via-generators)
    
      * [Pausing long-running tasks](http://exploringjs.com/es6/ch_generators.html#_pausing-long-running-tasks)
        
        ```
        run(countUp());

        function run(generatorObject) {
            if (!generatorObject.next().done) {
                // Add a new task to the event queue
                setTimeout(function () {
                    run(generatorObject);
                }, 1000);
            }
        }
        function* countUp(start = 0) {
            const counterSpan = document.querySelector('#counter');
            while (true) {
                counterSpan.textContent = String(start);
                start++;
                yield; // pause
            }
        }
        ```
    
      * [Communicating Sequential Processes (CSP)](http://exploringjs.com/es6/ch_generators.html#sec_csp)
      
        ```
        import csp from 'js-csp';

        csp.go(function* () {
            const element = document.querySelector('#uiElement1');
            const channel = listen(element, 'mousemove');
            while (true) {
                const event = yield csp.take(channel);
                const x = event.layerX || event.clientX;
                const y = event.layerY || event.clientY;
                element.textContent = `${x}, ${y}`;
            }
        });

        function listen(element, type) {
            const channel = csp.chan();
            element.addEventListener(type,
                event => {
                    csp.putAsync(channel, event);
                });
            return channel;
        }
        ```

* ES Callbags
  
  * [Why we need Callbags](https://staltz.com/why-we-need-callbags.html)

* ES flow  
  callbacks -> promises -> generators -> async/await
  
* [.NET Pipelines](https://msdn.microsoft.com/en-us/library/ff963548.aspx)

* [PyToolz](http://toolz.readthedocs.io/en/latest/index.html)

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

* https://github.com/conal/talk-2015-essence-and-origins-of-frp

* 
