# Async Using Fibers

A proposal for a simple api to introduce async functionality to wren, with minimal changes to the core VM

<!-- vim-markdown-toc GFM -->
* [Motivation](#motivation)
   * [Async vs Concurrency](#async-vs-concurrency)
* [Proposal](#proposal)
   * [Example](#example)
   * [API](#api)
      * [Async](#async)
      * [Asyncable](#asyncable)
* [Implementation](#implementation)
* [Alternatives](#alternatives)

<!-- vim-markdown-toc -->

## Motivation
It would be desireable for wren to have some supourt for asyncronous actions to allow wren to efficiently do I/O. However, wren is designed with simplicty of implementation in mind, and we want to avoid making any un-nescisary additions to the core VM. Indeed, a host application (e.g. a game engine) might handle asyncronicity itself. Therefore this proposal should be considered as primarity focsed on the CLI, and try to minimise changes to the core VM.
The VM itself does not even need to have a concept for asyncronicity. 

### Async vs Concurrency
Wren currently has first class Concurrency supourt with `Fibers`, these allow execution of one fiber to be temporarily suspended while we execute a different fiber. This is different to Asyncronicity, in which we would suspend a fiber while we wait for some process outside of normal wren execution (eg: network IO)

## Proposal
Create a new builtin class: `Async`, that uses fibers for asyncronous programming

### Example
A toy example of how `Async` could be used to make an http request

   :::wren
   var x = Async.new {
      //here Http is an imaginary http client
      var url = "https://wren.io"
      var response = Fiber.yield(Http.get(url))
      System.println(response.body)
   }

   System.println("I'll just do some stuff here while I wait")
   // ...do other stuff...
   System.println(x.join())

### API
#### Async
+ `Async::new(x)`: constructor for `Async`, performs the opperations in `x` up to the first `Fiber.yield(_)`, when it returns execution to the parent fiber
+ `Async::join()`: suspends the current fiber until `x` has finished executing.

#### Asyncable
Any object that is yielded from an `Async` execution flow must have the following method: `foo.then(_)` to allow `Async` to return flow to it

## Implementation

## Alternatives

[sagas]: https://github.com/redux-saga/redux-saga
[async]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
