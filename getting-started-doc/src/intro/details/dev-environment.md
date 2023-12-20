# DevEnv (dev-environment)

The dev-environment is also dubbed "devenv". It is a directory structure suited to hold the configuration and data for a one of your development projects or tasks. Typically, different projects are isolated from each other by their dev-env, but it is no problem to fine-tune this isolation. 

A dev-env has the following structure:

```plain
├── dev-environment.yaml
├── artifacts
│   ├── inst
│   └── repository-configuration.yaml
├── commands
│   └── setup-main.yaml
├── eclipse-workspace
├── git
└── tf-setups
    └── main
```

* **artifacts** is a directory containing the configuration and local storage for artifact resolution and installation.

* **artifacts/inst** is the directory to be used by default for local artifact installation (of course, also used for dedicated resolution)

* **artifacts/repository-configuration.yaml** is the config file for artifact resolution and installation. [More details...](#configuration)

* **commands** contains individual jinni alias macros. Each is contained in a yaml file and is a list of jinni commands. Within a dev-env those aliases are always found. 

* **dev-environment.yaml** is a marker to indicate a dev-env

* **eclipse-workspace** contains your (pre-configured) eclipse workspace

* **git** contains one or multiple git repositories with  your actual project data

* **tf-setups** is the default destination for local server installations (e.g. tomcat)

* **tf-setups/main** is the dedicated place for the standard tomcat server to be installed in the project. 



# Configuration

The file `dev-environment.yaml` is empty and just a file-system marker to indicate the base folder of a dev-env.


The `artifacts/repository-configuration.yaml` contains the following most relevant properties:


| name | mandatory | description |
|---|---|---|
|cachePath|yes| a local file system path for remote repository caching|
|installRepository|no|a local file system repository for local installation of build products|
|uploadRepository|no|a repository for dedicated artifact *uploads*|
|repositories|yes|a list of repositories for dependency resolution|

You may use environment variables like this `${env.YOUR_VARIABLE}`. The variable `${config.base}` is replaced by the location of the config file. 

The files in `commands` are jinni alias macros/scripts in yaml format. They contain more complex jinni commands. Within a devenv the scripts located here can always be executed just with `jinni script-name`. 


***

## Tutorials

It is highly advised to learn the content of this documentation by going through a series of practical exercises. 

[Exercises...](../practice/devenv.md).

