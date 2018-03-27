# Async Using Fibers

A proposal for a simple api to introduce async functionality to wren, with minimal changes to the core VM

<!-- vim-markdown-toc GFM -->

* [Motivation](#motivation)
   * [Async vs Concurrency](#async-vs-concurrency)
* [Proposal](#proposal)
* [Implementation](#implementation)
* [Alternatives](#alternatives)

<!-- vim-markdown-toc -->

## Motivation
It would be desireable for wren to have some supourt for asyncronous actions to allow wren to efficiently do I/O. However, wren is designed with simplicty of implementation in mind, and we want to avoid making any un-nescisary additions to the core VM. Indeed, a host application (e.g. a game engine) might handle asyncronicity itself. Therefore this proposal should be considered as primarity focsed on the CLI, and try to minimise changes to the core VM.

### Async vs Concurrency
Wren currently has first class Concurrency supourt with `Fibers`,

## Proposal

```
var x = Async.new {
   var url = "https://wren.io"
   var webpage = Fiber.yield(Http.get(url))
   Fiber.yield(webpage)
}

System.println("I'll just do some stuff here while I wait")
// ...do other stuff...
System.println(x.join())
```

## Implementation

## Alternatives


[sagas]: https://github.com/redux-saga/redux-saga
[async]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
