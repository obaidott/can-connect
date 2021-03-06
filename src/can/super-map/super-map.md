@module {function} can-connect/can/super-map/super-map
@parent can-connect.modules

Create connection with many of the best behaviors in can-connect and hook it up to
a [can.Map](http://canjs.com/docs/can.Map.html).

@signature `superMap(options)`

  Creates a connection with the following behaviors: [can-connect/constructor/constructor],
  [can-connect/can/map/map],
  [can-connect/constructor/store/store],
  [can-connect/data/callbacks/callbacks],
  [can-connect/data/callbacks-cache/callbacks-cache],
  [can-connect/data/combine-requests/combine-requests],
  [can-connect/data/inline-cache/inline-cache],
  [can-connect/data/parse/parse],
  [can-connect/data/url/url],
  [can-connect/real-time/real-time],
  [can-connect/fall-through-cache/fall-through-cache],
  [can-connect/constructor/callbacks-once/callbacks-once].

  And creates a [can-connect/data/localstorage-cache/localstorage-cache] to use as a [can-connect/base/base.cacheConnection].

@body

## Use

The `can-connect/can/super-map` module exports a helper function that creates a connection
with the "standard" behaviors in can-connect and hooks it up to a
[can.Map](http://canjs.com/docs/can.Map.html) and [can.List](http://canjs.com/docs/can.List.html).

If you are using CanJS, this is an easy way to create a connection that can be useful and
fast in most circumstances.

To use it, first define a Map and List constructor function:

```
var Todo = can.Map.extend({ ... });
var TodoList = can.List.extend({Map: Todo},{ ... });
```

Next, call `superMap` with all of the options needed by the behaviors that `superMap` adds:

```
var todoConnection = superMap({
  idProp: "_id",
  Map: Todo,
  List: TodoList,
  url: "/services/todos",
  name: "todo"
});
```

As, [can-connect/can/map/map] adds CRUD methods to the `Map` option, you can use those to create,
read, update and destroy todos:

```
Todo.getList({}).then(function(todos){ ... });
Todo.get({}).then(function(todo){ ... });

new Todo({name: "dishes"}).save().then(function(todo){
  todo.attr({
      name: "Do the dishes"
    })
    .save()
    .then(function(todo){
      todo.destroy();
    });
});
```
