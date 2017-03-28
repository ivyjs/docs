# Configuration

All the required configurations can be found in `config` folder and `.env` file.

## .env file

Environment file can contain your confidential info, database credentials, api keys etc., because it is placed in `.gitignore`, therefore it will not be published on git, nor be publicaly available.
Properties inside are writted in the `key=value` way.

### Using env function

So how are we suppose to use the `.env` file values? Global function `env` is used inside of configuration files in order to get the value from `.env`.

```
...
  "port": env('PORT', 3000),
...
```

When we try to get the port property from the config file, it will first try to get `PORT` key from `.env` file, if there isnt `.env` file, or the `PORT` key isnt set, second argument represents the default value, so the `3000` would be used instead.

To set the `port` value in the `.env`, it should look like

```
PORT=80
```


## Get config value

`Config` service is used to get data from config files. You can access it by using its namespace `use('Config');`.
So lets say that we are looking for the application port. Path to that config value should be joined with `.` (dot).
First, we are looking for the file name where property is stored, and in this case, its `app.js`, we will only use the name of the file, without the extension.
After that, every level in config file object should be separated with dot. 

Getting the port value:
```
let Config = use('Config');
let port = Config.get('app.port');
```

What if we have multiple levels like:

database.js > adapter > mysql > user

```
let Config = use('Config');
let user = Config.get('database.adapter.mysql.user');
```
