# Local Installation for Debugging

Next we create an `Eclipse` project so we can run and debug our application from the IDE.

* Build and install all artifacts locally by running `dr`
  ```cli
  dr
  ```

  **Explanation:** Artifacts must be installed in the local repository (`hc-tutorial/repo`) as it's required by a later step - local installation with and creation of an `Eclipse` project for debugging.

* Configure our tutorial as the app to install in our `main` setup task and add a flag to create an `Eclipse` project for debugging as part of installation.

  Set `hc-tutorial/commands/setup-main.yaml` content to:
  ```yaml
  !com.braintribe.model.platform.setup.api.SetupLocalTomcatPlatform {
    # dependency on the tutorial project's setup
    setupDependency: "hc.tutorial:hc-example-setup#[1,2)",

    # dir where to install our application
    installationPath: "${config.base}/../tf-setups/main",

    # create an Eclipse project for debugging
    # it's name is derived from the setupDependency, i.e. hc.tutorial:hc-example-setup-debug
    debugJava: true,
  }
  ```

* Run `setup-main.yaml` with `Jinni` to install the application locally:
  ```cli
  jinni setup-main
  ```
  _**Note:** Yes, this YAML file  is resolved based on the passed argument, as any other file inside `commands` folder would be._

 * All done, our application is now installed in our `dev-env` under

  ```filesystem
  hc-tutorial/
      tf-setups/
          main/
  ```