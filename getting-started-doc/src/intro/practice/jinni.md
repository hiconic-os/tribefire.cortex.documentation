# Jinni tutorials

Here you will learn how to work with jinni, repositories, configuration and local development environments.

For jinni there is always a usage *context* given by the current directory location where a command is being executed. Various commands can draw information from a context. For example most of the `create-...` commands are used to create templated artifacts as a starting point for development inside the context of a [devenv](../details/dev-environment.md). 

Here we focus on very basic functionality in the context of a [DevRock-SDK](../details/devrock-sdk.md).

## Exercise 1

Read [introduction to jinni](../details/intro-jinni.md) for help. 

1. Study your version of jinni.

1. Get a list of all commands available in jinni.

1. Sometimes it may be necessary to update jinni. Run the script `jinni-update` in your terminal. You should get a response like this

    ```
    Checking for update:
    Current jinni version: 2.1.539
    Latest found jinni version: 2.1.541
    Extracting latest jinni version: 2.1.541
    Jinni prepared in: <path>/devrock-sdk/tools/jinni/jinni-update
    Transferring prepared Jinni to installation
    Update complete
    ```

    If you run `jinni print-version` afterwards, you should get the new version of jinni.

## Exercise 2

1. Create a [devenv](../details/dev-environment.md):  `jinni create-dev-env my-first-dev-env`

    - Collect your devenvs into one place. We suggest using the prepared directory `devrock-sdk/env/` for this purpose. 
    - Enter the directory `devrock-sdk/env`
    - `jinni create-dev-env my-first-dev-env`

    Note, foremost a devenv is a new context for jinni. Inside a particular devenv, jinni will use specific configuration files.  

1. Check that the new directory `my-first-dev-env` was created. Look at the content and compare to [devenv](../details/dev-environment.md).

1. Now enable the **verbose** mode via jinni `options`:

    ```
    jinni create-dev-env my-second-dev-env : options -v
    ```

    Study the differences in response, there is additional information provided now. 

    Many jinni commands report additional information when the verbose flag is set. 

## Exercise 3

1. Run `jinni history`. It should contain one item like

    ```plain
    History Entry #N:

    Filename: print-version.20230501123713.yaml
    Executed: Montag, 1. Mai 2023 um 12:37:13 +02:00
    Content: !com.braintribe.model.jinni.api.PrintVersion {}
    ```

    corresponding to the `print-version` jinni command you called earlier. It has a specific history entry number `#N`. 

1. Repeat the previous `print-version` command using `jinni history -r N`.   

    For more complex commands this can be of significant help. 

