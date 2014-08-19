Routing
=======

Routing is a common pattern, used in almost everyone of our applications, but often times it is seen as a magical process. There is nothing magical about it and nothing to be afraid of when approaching it.

There are several forms of routing, but they mostly boil down to:

1. Storing a pattern
1. And, assigning a function or callback that gets executed when that pattern
   is matched

The pattern can be an absolute string match:

```
"My name is John" == "My name is John"
```

A tokenized string match:

``` javascript
var routes = [
  {
    pattern: "My name is :firstName",
    callback: function (firstName) {console.log("My name is",
firstName);},
    regexp: /^My name is (.*)$/
  }
];

var matchingRoute = routes.filter(function(route){"My name is John" ~= route.regexp})[0];
```

Or variants of other pattern indicators such as an http request for a resource:

``` javascript
// GET /posts/1
var routes = [
  {
    method: "GET",
    pattern: "/posts/:id",
    callback: function (postId) {},
    regexp: /^\/posts\/(\d*)$/
  }
];
// et al
```

The key is, routing is about storing away patterns, finding a way to tokenize the strings if you need that, and calling the callback when a pattern has matched. It doesn't matter what language you are coding in, nor what application you are shooting for, it is always going to be a variant of this theme.

A developer will be tempted to use a long list of procedural switch or if statements at one point or another in their life, such as this:

``` javascript
var request = {method: "GET", path: "/posts"}; // This is just a sample of what a request could look like coming in to a server

if(request.path == "/posts") {
  if(request.method == "GET") {
    console.log("Here's your post index");
  } else if(request.method == "POST") {
    console.log("Here's the new post you asked for");
  }
}
// et al
```

This gets horribly complex with each new nested condition you add. A router is meant to abstract those conditions away so that your code is:

1. More managable
1. Less error prone
1. Easier to understand

Wouldn't something like this be more beneficial in the long run?

``` javascript
var request = {method: "GET", path: "/posts"}; // This is just a sample of what a request could look like coming in to a server
var router = new Router();

router
  .get("/posts", function () {
    console.log("Here's your post index");
  })
  .post("/posts", function () {
    console.log("Here's the new post you asked for");
  });
```

Of course this is just a coarse sample. Imagine building an entire API with both approaches. Which would you rather come back to a month later when changes are needed?
