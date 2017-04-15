# Routing

Creating routes in the application can be done by editing `routes/routes.js` file. 
`Route` object have methods to create routes which corresponds to the route method.
First parameter is always the route path, second is the route closure, and third (optional) are the route options.
Parameters are binding using the prefix `:`, and they are sent to the closure as the first argument.
So by using `/:id`, and hitting the route `/3`, you will get parameter `{ id: 3 }` for example.


## GET

```
Route.get('/:id', function(parameter) {
  return parameter.id;
});
```

## POST

```
Route.post('/user', function(parameter) {
  return "This is user post method";
});
```

## PUT

```
Route.put('/user', function(parameter) {
  return "This is user put method";
});
```

## DELETE

```
Route.delete('/user', function(parameter) {
  return "This is user delete method";
});
```

## Binding to the controller

In order to make things more clear, the concept of the [controller](/docs/controller) is introduced. To forward your route request to the controller, make the 2nd argument of route in form of `{ControllerName}@{methodToTrigger}`.

```
Route.get('/users', 'UserController@index');
```


# Options

Options are optional route parameter which sets additional parameters to the route.

## Middlewares

Middleware option can use either array of middleware or a single one.

```
Route.get('/home', function() {
  return "this goes through middleware";
}, { middleware: 'auth' });
```

This request will go through the middleware auth before reaching route closure.

You can specify multiple middleware as well.

```
Route.get('/home', function() {
  return "this goes through multiple middleware";
}, { middleware: ['auth', 'www'] });
```

# Route list

To view the list of all routes, ivy comes with the cli helper.
Run the command `node ivy route:list` in the root of your project, and it will print out the list of routes.

# Object response

Nodejs works with json very well, thats a well known fact, but you can't send raw json object as the response, cause only string is applicable. Ivy solves this issue by casting object to string, and returns the respose of `application/json` type.

```
Router.get('/json', function() {
  return {
   "good": "testing",
   "is": "here"
   });
```

will actually work here!

# Route parameters

To understand better how are we dealing with the parameters, lets see the example:

```
Route.get('/user/:id/:action', 'UserController@actionHandler');
```

Now that our route is defined, lets see the `actionHandler` in the `UserController`:

```
actionHandler(request) {
  console.log(request); // { "id": 3, "action": "create" }
}
```

# Resources

We already saw that [controller](/docs/controller) can be created as a resource right away, but what about routes? That also works!

```
Route.resource('user', 'UserController');
```

function `resource(resourceName, resourceHandlerController, resourceOptions)` will create all relative REST routes for a given resource. By triggering command `node ivy route:list` we will see the list of them:

```
Method Route                    Handler               
------------------------------------------------------
GET    user                     UserController@index
GET    user/:id                 UserController@show
POST   user                     UserController@create
PUT    user/:id                 UserController@update
DELETE user/:id                 UserController@remove
```
