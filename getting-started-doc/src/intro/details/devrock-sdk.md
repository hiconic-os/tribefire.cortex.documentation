# Introduction to Devrock-SDK

The Devrock-SDK developer package includes three things:
1.  The build system (ant) with extensions.
2.  The jinni command line tool, which is your way to send requests to and receive responses related to development and the platform. 
3.  Configuration files. 
 
# Devrock-SDK Structure

```plain
	devrock-sdk
	|
	├── conf 
	│   ├── repository-configuration-devrock.yaml
	│   └── templates
	├── env
	├── repo
	└── tools
	    ├── ant
	    ├── ant-libs
	    └── jinni
```

* The `repository-configuration-devrock.yaml` is the yaml representation of a configuration object of type `com.braintribe.devrock.model.repository.RepositoryConfiguration` with two mandatory properties

    - cachePath: "${config.base}/../repo"
    - repositories: a list of repositories for resolution
		- "devrock" for platform tools
		- "core-dev" for access further platform functionality 

    The `cachePath` is the local cache of the remote repositories. It is initially empty. Relative paths can be used using `${config.base}`, pointing to the path of the config file. 
    
* The `env` directory is where your projects can be stored. It is best-practice to use individual [dev-environment](dev-environment.md)s (aka "dev-env") for each project. It is not mandatory to use the `env` directory. You may create another location elsewhere for the same purpose with no disadvantage. 

* The `repo` directory is the local cache for remote repositories. Note: make sure that your respective `repository-configuration.yaml` files actually point to this directory using `cachePath`. This is not automatic, but rather a useful convention. 

* In `tools/ant` we deliver a version of `ant`, but we offer a wrapper script `dr` which will call `ant` in the right way. 

* In `tools/ant-lib` there are custom extensions to `ant`

* In `tools/jinni` we provide the jinni command line tool

The special wrapper around `ant` at `tools/jinni/bin/dr` will automatically use the provided `ant-lib` extensions, the provided `conf` folder, and the `repo` cache folder. So, if you use the developer package and need to compile something with ant, just use `dr`. 


__Further reading:__
  - [Configuration](configuration.md)
  - [What is an "dev-environment, aka devenv"?](dev-environment.md)
