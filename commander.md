# Ivy's commander

To help you out when it comes to developing your application, Ivy comes with user friendly command-line interface.
Commander is accessable by running `node ivy` in root directory of your project.

Help for each command is available with `--help` parameter, so `node ivy make:middleware --help` will display a help message of command, together with usage example and options.

## Creating commands

Making commands for Ivy's commander is done using the 'Ivy/Commander' namespace.

```
let Commander = use('Ivy/Commander');

Commander.register('my:command')
         .description('It does something cool')
         .usage('my:command {cool_stuff}')
         .option('--red', function() {
            console.log('My red text option.');
         }, 'Description of red option.')
         .execute(function(command) {
            console.log('This function is executed when command is run');
            console.log('command.parameteres are having the array of parameters provided');
            console.log('Cool stuff is: ' + command.parameters[0]);
         });
```

### .register(command_name)

By passing command name to the register function, we are setting the name property of our brand new command.

### .description(description_text)

Short description text, its displayed in the `help` menu of cli, as well as on `--help` menu of command.

### .usage(example)

Provide an example usage of command.

### .option(option_signature, callback, description_of_option)

Option signature stands for the string passed to the command. If we call our command as `my:command --red` function that is going to be executed prior the callback of command is the option callback function, which is supplied as the 2nd parameter.
Description of option is displayed under help menu of command.

### .execute(callback)

Last and most important is the `execute` function, which has callback function as parameter. Callback function is going to be executed once command is triggered, and as parameter theres a command object passed through. Note that command object also has the `parameters` array, which consists of additionl parameters sent through the command.
