# Creating Artifacts

Using `Jinni` we start by creating a **new dev-env** and inside of it create all the artifacts that make up an extension.

* Open a terminal inside `devrock-sdk/env` directory. 

* Create a new dev-env called `tf-tutorial`:
  ```cli
  jinni create-dev-env tf-tutorial
  ```

  Expected file structure:
  ```filesystem
  tf-tutorial/
      artifacts/
      commands/
          setup-main.yaml
      eclipse-workspace/
      git/
      tf-setups/
      dev-environment.yaml
  ```

* Navigate to `tf-tutorial/git`:
  ```cli
  cd tf-tutorial/git
  ```

* Create a new directory `tf.tutorial` for your code:
  ```cli
  mkdir tf.tutorial
  ```

  _**Note:** This directory is both a git repository and an artifact group, i.e. it's name will be used as a group in the `pom.xml`s of our artifacts._

* Navigate to this `tf.tutorial`.
  ```cli
  cd tf.tutorial
  ```

* Create a `Tribefire` extension with a sample `Service Processor`:
  ```cli
  jinni create-extension tf-example --samples all 
  ```

  _**Note:** We use `--samples all` which for now only creates a `ServiceProcessor`, but will later involve more samples._

  Expected file structure:
  ```filesystem
  tf.tutorial/
      parent/
      tf-example-api-model/
      tf-example-deployment-model/
      tf-example-doc/
      tf-example-initializer/
      tf-example-module/
      tf-example-processing/
      tf-example-processing-test/
      tf-example-setup/
      build.xml
  ```