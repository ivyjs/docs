# Middleware

Middleware is located before your route request closure, so it provides a great way of filtering/editing/parsing your request before it gets to the request handler.

## Creating middleware

Creating a middleware can be done with a simple command `node ivy make:middleware {name}`, and it will automatically generate a middleware file with a desired name in the folder `/app/middleware`.  
After thats done, we should register it in the `config/middleware.js` with name and namespace.

Lets say that we need a middleware `TestMiddleware`, first, we are going to create it with `node ivy make:middleware TestMiddleware`  
and it will create file `app/middleware/TestMiddleware.js` for us.

```js
bind('App/TestMiddleware', function () {
    return function (data, next) {
        next();
    }
});
```

so, we've got the middleware, whats next? Lets register it under `config/middleware.js`.

```js
module.exports = {
    /**
     * List of middleware in form of:
     * binding: namespace
     */
    'middlewares': {
        ...
        'test': 'App/TestMiddleware'
        ...
    }
    ...
```

`'test'` is the name of the middleware that we are going to use in route, to request it.

Assign it to the route by adding middleware option

```js
Route.get('/home', function() {
  return "through the middleware!";
}, { middleware: 'test' });
```

## Errors

Any error messages that are sent from the middleware, can be passed as an argument to the `next` function. After message parameter is added, the request does not go further, but returning the parameter sent using `next` to the client.

```js
bind('App/ErrorMiddleware', function () {
    return function (data, next) {
        next("this is error message");
    }
});
```

User will get response to this route `"this is error message"`, and the request will never hit the route handler.

## Groups

Sometimes you might require multiple middleware for a route, instead of writing a list of options for route like `{ middleware: ['auth', 'token', 'another'] }`, we can define a group of middlewares.

This can be done in the `config/middleware.js` file by adding a key:value in groups.

```js
"groups": {
  ...
  "web-group": ['auth', 'token', 'another'],
  ...
}
```

now, our route can use `{ middleware: "web-group" }`. Also, make sure that you have previousely registered every middleware that is used in the group.

