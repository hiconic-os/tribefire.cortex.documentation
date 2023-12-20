# Migrating from a custom setup to DevRock-SDK

Follow the steps described in [Setup DevRock-SDK](setup-sdk.md). 

**Unset** in your environment (system dependent):

- the `PATH` pointing to old scripts and installations, 
- `ANT_HOME` and
- `ANT_LIB_DIR` since they are set inside `dr`. 


On a typical command line terminal (depending on your system, you may have to re-login to get an updated environment) and on Windows prompt you have to use the "bat" versions. 

- make sure that `which jinni` and `which dr` point to the correct scripts. One Windows you may use `where jinni` and `where dr`.

- run `jinni` and check for the expected version.

- go to a temporary directory (and delete afterwards) and issue `jinni create-model test-devrock` and see if there are no errors. THEN check, that in your cache-directory `devrock-sdk/repo` the following artifacts have been downloaded: `tribefire/cortex/assets/templates/model-priming-template`, `com/braintribe/devrock/templates/build-system-template`, `com/braintribe/devrock/templates/project-metadata-template` and `com/braintribe/devrock/templates/source-control-configuration-template`

