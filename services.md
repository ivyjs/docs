# Services

Ivy includes a great and easy way of manipulating your services, together with performing some tasks like dependency injection.

## Binding

Registering a service is done by using bind method.
First parameter should be a namespace of a given service, which will be binded to it, while second is a closure which is suppose to return a new instance of service.

```
bind('Ivy/CoolService', function() {
  return new CoolService();
});
```

### Singleton

You can also directly bind a singleton object, by using singleton method.

```
singleton('Ivy/SingletonService', function() {
  return new SingletonService();
});
```

### Namespace

Javascript doesn't come with the namespaces, however, Ivy does, and they provide you a handy way of working with your classes and objects.
Global function `namespace`, requires 2 arguments, one is the desired namespace, while the second is the class binding.

```
class Model {
  great() {
    return "this is cool!";
  }
}

namespace('Ivy/Model', Model);
```

## Alias

You can also alias your namespaces.

```
alias('Ivy/Alias', 'Ivy/Real/Namespace');
```

Note that this is available by editing the `services` config file, more about it comes later.

## Use

So, until now, we were talking about binding a namespace to the closure, but how are we suppose to get the binded object?

```
let obj = use('Ivy/Model');
```

and thats pretty much it. However, make sure that you understand few things.
First, in case that we have used a `bind` or `singleton` function to bind a given namespace, `obj` will contain the instantiated object of a service.
Second, when namespace is registered with `namespace` function, it will return only a class, so you would still need to do the `new` part.
And third, if theres an alias for that namespace, you can use it as a parameter, so `use('Ivy/Alias');` is just fine.

### Injection

By combining `use` and `bind` / `singleton` functions, we are able to perform the dependency injection in the binded class.

```
bind('Ivy/CoolService', function() {
  return new CoolService(use('Ivy/Dependecy1'), use('Ivy/Dependency2'));
});
```


## Services config file

`config/services.js` has a list of service files that are being loaded on application bootup, as well as the list of aliases that are being created.

```
/**
 * Load application providers.
 */
'providers': [
    ...
    modules_path() + '/ivyframework/src/Config/ServiceProvider',
    ...
 ],
 ...
```

In case that you have a service provider file which you would like to be loaded during the application startup, put his path in the list of providers.

```
/**
 * Create a desired aliases.
 */
'alias': {
    ...
    'Config': 'Ivy/Config'
    ...
}
```

Aliases are created by writing a simple key: value in the list. Key is an alias, while value is the real namespace.
