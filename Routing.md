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
