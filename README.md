# Installation
Setting up the IvyJS is pretty straight forward. The main and the only requirement is Nodejs with version >= 7.0.0, you can download it from the official [website](https://nodejs.org/).

## Ivy setup
Ivy projects are created using Ivy CLI, which you can get from npm.
So, add it globaly by doing:

`yarn global add ivy-cli`

alternatively, if you are using npm as a package manager run:

`npm install -g ivy-cli`

Thats it!

After thats done, `ivy` command is going to be available globaly on your system.
To create a new project, run the command `ivy new {project name}`, for example `ivy new example` will create a new folder called `example` which contains the fresh setup of ivy project.

## Running app

For the development we would recommand something like `nodemon` package from npm, which will run auto restart on detected change.
To run the application, use `node .`. After that, application is available on the `port` you setted in config/`.env`, by default its `3000`, so hit the `http://localhost:3000/` to see the homepage.
