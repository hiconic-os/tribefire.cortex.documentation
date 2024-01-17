# Introduction to jinni

`jinni` is the command line interface to send requests to and receive responses from the underlying platform. 

Commands are any `ServiceProcessor`s that have been made known to the jinni terminal. 

Requests are entity types with properties that represent arguments of that request. Using jinni one can set these properties using the posix command line argument syntax `--property <value>`. 

Running a command with jinni, type `jinni <command>`. 

An important command is `help`. Try `jinni help`. 

It is relevant to point out here, that the help command is based on the self-reflection of the platform and automatically provides the correct output. 

This becomes even more clear when you try `jinni help <command>` (for example `jinni help get-artifact-versions`) it will automatically reflect the properties of the request object to provide documentation on how to configure the command using jinni.

Some request types have parts of their properties marked as positional arguments which means that they can be passed in order without `--property`. Lets take the concrete example of the  request `get-artifact-versions` which has a property `artifact` marked as positional argument. Jinni reflects about this in its help syntax section. 

Try a concrete command execution with a positional argument:

```plain
jinni get-artifact-versions tribefire.extension.setup:jinni
```

to get a list of available versions of jinni itself. This data is retrieved from the remote repositories -- without downloading any real artifact data.

## Provide further context via `options`

Jinni `options` provide powerful possibilities to fine-tune how jinni commands work. 

Try `jinni help options` for a full list. 

The correct way to provide `options` for a jinni command is to chain it like this

```plain
jinni command <command-properties> : options <options-properties>
```

Examples of what can be done are:

- switch on verbose output with `options -v`
- use specific repository configuration `options --repositoryConfiguration <path-to-yaml>`
- echo command in YAML syntax: `options -e`
