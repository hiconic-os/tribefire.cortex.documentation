# Further information

The DevRock-SDK first of all provides you with access to the binary artifact repositories used by the platform for almost anything. 

You can modify the repository configuration to include your own private repositories, too. 

Repositories of maven layout are supported and can be hosted on all suitable providers, or also in local directories. 

In general, the SDK only provides a *best practice* and you are free to setup the tools and configuration in another custom way. However, please understand that for a custom setup fixing of problems may be much harder and help will be limited. 

## Configuration

### Repository configurations

The config file `conf/repository-configuration-devrock.yaml` is used by build tools (jinni, build system) to pull additional build artifacts, build scripts, templates, etc. This is done via the environment variable  `REPOSITORY_CONFIGURATION_DEVROCK_ANT_TASKS`, which is automatically set if you use the SDK inside the `dr` script, and the config file `conf/artifact-templates-configuration.yaml`. 

In the SDK, all repository caches are (best) configured to point to the same path, i.e. at `devrock-sdk/repo`. This saves disk space and minimizes the need for downloading remote data since it can be reused. 


### Devenv creation

One of the main tasks of the sdk is to facilitate the setup of [devenv](dev-environment.md)`s. While the SDK provides the main tools, a devenv is your everyday's development environment for your concrete project. 

A new devenv can be created with `jinni create-dev-env <name>` and will come with a dedicated `artifacts/repository-configuration.yaml` and also a default Eclipse workspace configuration in `eclipse-workspace`.

You may tune the generation of new devenvs to your requirements by modifying the SDK `tools/jinni/conf/dev-env-generator-config.yaml`: 

- **eclipseWorkspaceTemplate** is the path to your desired Eclipse workspace template configuration. The SDK provides a suited version with many good settings in `templates/eclipse-workspace`, which therefore is the default. 

- **repoConfTemplate** is the path to your repository-configuration template. The SDK comes with `templates/repository-configuration-devenv-hiconic-os.yaml`, which points at the `GitHub` Maven repository of [hiconic-os](https://github.com/hiconic-os) and requires a [Personal Access Token](https://github.com/settings/tokens) with (at least) `read:packages` scope for the `GITHUB_READ_PACKAGES_TOKEN` environment variable.

### Build system

If you use the SDK, the build system extensions (currently ant libs) are located at `tools/ant-libs` and are configured via the `dr` script. There is an additional config file at `conf/devrock-ant-tasks-configuration.yaml` for access from within platform code. 

### Jinni logging

In `conf/logging.properties` the logging setting of jinni can be adapted. 


__Further Reading__:
- [MCng configuration](https://eclipse.modularmind.eu/documentation/mc-core/mdoc/com.braintribe.devrock/mc-core-documentation/configuration/configuration.html) 
