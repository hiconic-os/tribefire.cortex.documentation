# Introduction of the platform explorer

The explorer is a web GUI that runs in a dedicated server. It is used for platform administration, management and overview. 

See [Explorer Documentation](https://documentation.tribefire.com/tribefire.cortex.documentation/concepts-doc/features/ui-clients/explorer.html) and 
[Using Control Center and Explorer](https://documentation.tribefire.com/tribefire.cortex.documentation/tutorials-doc/control-center/using_control_center.html) for further information. *NOTE* this quickly drags you very deeply into platform technology and you will need further learning to understand all the advantages. 

## Run the explorer
  - create  an `explorer-demo` [devenv](dev-environment.md) inside the `devrock-sdk/env` directory for better encapsulation:
    - inside directory `devrock-sdk/env`
    - `jinni create-dev-env explorer-demo`
    - `cd explorer-demo`
  - run inside `devrock-sdk/env/explorer-demo` the command `jinni setup-local-tomcat-platform --installationPath tf-setups/main --setupDependency tribefire.setup.classic:standard-setup#3` 
  - start server: `tf-setups/main/runtime/host/bin/startup.sh`
  - connect to server with web browser at `localhost:8443` login with `cortex`/`cortex`
  - study platform reflection
  - stop server: `tf-setups/main/runtime/host/bin/shutdown.sh`


