# First experience with dev-environment

Here you will learn how to practically work with a [dev-environment](../details/dev-environment.md) (devenv). 

## Excercise 1

In a devenv you can provide new jinni commands (like scripts) by providing one or several commands in serialized yaml format. 

The information needed for writing such scripts can be obtained from `jinni help <command>` since this will printout the qualified name of the command and also a  description of all properties. The *mandatory* properties must be included in the yaml script, the *optional* properties only if needed. 

The advantage of the `command` path inside a devenv is that jinni is configured to automatically use commands located there. So this is very convenient to store often repeated commands. 

With the `jinni --fromFile <script.yaml>` you can also run scripts from concrete yaml files. 

1. Create a new devenv, name it *jinni-ex1*. Remember: put all your devenvs **inside** `devrock-sdk/env`.

1. Create a new command in the `commands` directory of the *jinni-ex1* devenv, which sets up an [explorer GUI](../details/intro-explorer.md). If you need hints, look at the existing `commands/setup-main.yaml` 
    1. Name your command *setup-explorer.yaml*
    1. Execute your command by running `jinni setup-explorer`
    1. Start the explorer GUI (see [explorer GUI](../details/intro-explorer.md)) and browse it with firefox. 

1. Explain a likely useful purpose of `commands/setup-main.yaml` that explains why it is included in all devenvs by default. 


## Excercise 2

Jinni provides a nice interface to work with artifact repositories. Use it to manage your repositories, browse them and curate their content. 

It is good practice to not directly pull third party dependencies from maven central or other public servers, but to maintain private repositories with well controlled dependencies that are manually updated. 

Here you will learn how to do this with jinni. 

1. Create a new devenv with name *devenv-ex2*. Remember: put all your devens **inside** `devrock-sdk/env`.

1. Edit the repository configuration file of the *devenv-ex2* devenv located in the `artifacts` folder. 

    1. Change *cachePath* to *${config.base}/cache* and create the directory `artifacts/cache`

    1. Remove 
        1. the *install repository* and its references.
        1. the standard repositories *core-dev* and *third-party*. 

1. Create a new `MavenHttpRepository` inside the *repositories* list
    1. name: *central*
    1. url: *https://repo1.maven.org/maven2/*
    1. restSupport: *none*

1. Create a new `MavenFileSystemRepository` as property *uploadRepository*
    1. name: *myrepo*
    1. rootPath: `${config.base}/myrepo`
    1. cachable: false
    1. create the directory `artifacts/myrepo`

1. Now we study some packages on maven central, e.g. `jinni get-artifact-versions "org.apache.arrow:arrow-tools"`. You must get a list of versions found on Maven central. Pick any (recent) version of the library, e.g. *11.0.0*. 

1. Download this version, check the `jinni help get-artifacts` command for help. 

    1. Create target directory `download`. Use `jinni  download-artifacts -a "org.apache.arrow:arrow-tools#11.0.0" -p download`

    1. Study the content of the `download` and the `artifacts/cache` directories. Both will now contain the version of the artifact you selected. The former because this is your target, the latter since all remote content is cached there. 

    1. Let's also look at *license* information, which is highly advised in general. Add the `-l true` flag to the `download-artifacts` command. In addition, you will now see license details for each downloaded artifact. 

    1. Often one artifact requires further transitive artifacts. Also add the `-t true` flag to the `download-artifacts` command to get a full transitive download. You will also get a complete dependency resolution tree. 

1. Use the jinni `upload-artifacts` command. First study it with `jinni help`.

    1. Perform upload into your *uploadRepository* *myrepo*, which is empty so far, with `jinni upload-artifacts -p download`

    1. Now your directory `artifacts/myrepo` will contain all the selected artifacts. Note, that the *uploadRepository* can of course also be a remote *MavenHttpRepository*. 



