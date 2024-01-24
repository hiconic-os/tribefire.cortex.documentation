# Creating Artifacts

Using `Jinni` we start by creating a **new dev-env** and inside of it create all the artifacts that make up an extension.

* Open a terminal inside `devrock-sdk/env` directory. 

* Create a new dev-env called `hc-tutorial`:
  ```cli
  jinni create-dev-env hc-tutorial
  ```

  Expected file structure:
  ```filesystem
  hc-tutorial/
      artifacts/
      commands/
          setup-main.yaml
      eclipse-workspace/
      git/
      tf-setups/
      dev-environment.yaml
  ```

* Navigate to `hc-tutorial/git`:
  ```cli
  cd hc-tutorial/git
  ```

* Create a new directory `hc.tutorial` for your code:
  ```cli
  mkdir hc.tutorial
  ```

  _**Note:** This directory is both a git repository and an artifact group, i.e. it's name will be used as a group in the `pom.xml`s of our artifacts._

* Navigate to `hc.tutorial`:
  ```cli
  cd hc.tutorial
  ```

* Create an extension with a sample `Service Processor`:
  ```cli
  jinni create-extension hc-example --samples all
  ```

  _**Note:** We use `--samples all` which for now only creates a `ServiceProcessor`, but will later involve more samples._

  Expected file structure:
  ```filesystem
  hc.tutorial/
      parent/
      hc-example-api-model/
      hc-example-deployment-model/
      hc-example-doc/
      hc-example-initializer/
      hc-example-module/
      hc-example-processing/
      hc-example-processing-test/
      hc-example-setup/
      build.xml
  ```