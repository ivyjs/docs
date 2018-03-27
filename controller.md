# Controllers

Controllers are classes used to help you with handling your route request.   
A new controller can be created using a command `node ivy make:controller {controllerName}` in project root.

```
node ivy make:controller UserController
```

will generate a file `app/controllers/UserController.js`.

## Request handlers

Functions defined in the controller can be used to handle your request on the same exact way as [Route](/docs/routing) callback works.  
So, we've got `UserController` previousely created, lets add index route handler there.

```js
class UserController {
  /**
   * This method returns the list of users.
   * 
   * @return {}
  **/
  index() {
    return [
      { name: "Adam", age: 23 },
      { name: "Joe", age: 25 },
      { name: "Phoebe", age: 20 }
    ];
  }
}

namespace('App/Controller/UserController', UserController);
```

We made a method in the controller, what now?  
All thats left to be done is to create a new route for that method in our [routes.js](/docs/routing) file.

```js
Route.get('/users', 'UserController@index');
```

Right now, after we hit the route `/users` we will get the json response containing the values returned from the controller's method `index()`.

Making your request use Async/Await is as simple as adding `async` to the handler function.

```js
async index() {
    return await fetchUserData();
  }
```

## Resource

The thing you will, most likely, do very often is performing CRUD \(Create, Read, Update, Delete\) operations. And, guess what? Ivy can help you with that as well.  
Creating CRUD controller is done with `--resource` option for the commander.

```
node ivy make:controller UserController --resource
```

will generate `app/controllers/UserController.js` containing all the relevant methods for that resource

```js
class UserController {

    /**
    * Show all the results.
    **/
    index() {

    }

    /**
    * Show resource.
    *
    * @param request
    **/
    show(request) {

    }

    /**
    * Creates a resource.
    *
    * @param request
    **/
    create(request) {

    }

    /**
    * Updates a resource.
    *
    * @param request
    **/
    update(request) {

    }

    /**
    * Delete a resource.
    *
    * @param request
    **/
    remove(request) {

    }
}

namespace('App/Controller/UserController', UserController);
```



