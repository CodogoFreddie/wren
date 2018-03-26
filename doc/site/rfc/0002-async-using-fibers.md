# Async Using Fibers

Similar to [redux sagas][sagas]

```

var x = Async {
   
   var url = "https://wren.io"

   var webpage = Fiber.yield(Http.get(url))

   Fiber.yield(webpage)

}

System.println("I'll just do some stuff here while I wait")

// ...

System.println(x.join())

```

[sagas]: https://github.com/redux-saga/redux-saga
