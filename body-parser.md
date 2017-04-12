# Body parser

When sending a request that includes body parameters (POST, PUT etc.), you will need to get that body parsed to object in order to work with it.
Middleware `'body-parser'` can handle that operation for you.

By setting route middleware with `{ middleware: 'body-parser' }`, you will get your route body data passed to the route callback parameter.

Fields that are sent through the middleware will be located in `body` property of parameters.

For instance, lets assume that we want to send this JSON object through the POST request body:
```
{
  "name": "Jack",
  "lastname": "Jackson"
}
```

to the route `/user`:

```
Route.post('/user', 'UserController@create', { middleware: 'body-parser' });
```

`create` method of `UserController`:

```
create(data) {
  console.log(data.body.name); // "Jack"
  console.log(data.body.lastname); // "Jackson"
}
```
