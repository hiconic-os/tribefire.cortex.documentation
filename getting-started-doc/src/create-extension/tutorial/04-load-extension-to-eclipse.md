# Eclipse Preparation

Each dev-env comes with its own `Eclipse` workspace. Let's open it from `Eclipse` menu `File/Switch Workspace/Other...` and picking the `hc-tutorial/eclipse-workspace` folder.

Let's now make sure we are running with Java 21, because (as of January 2024) Eclipse comes with Java 17:
* From the top menu let's go to `Preferences`
  * `Window` / `Preferences` on Windows / Linux
  * `Eclipse` / `Preferences` on Mac
* Navigate to `Java` / `Installed JREs`
* Make sure your `Java 21` is on the list and checked

From our new workspace import the following projects:
* `hc-example-api-model`
* `hc-example-processing`
* `hc-example-processing-test`
* `hc-example-setup-debug`

Do it by pressing `CTRL + SHIFT + I`, typing `hc-` in the dialog and selecting the projects.

_**Note:** This import feature, including the shortcut, comes from one of the `Devrock` plugins._

![](../images/import-projects.png)

The content of our workspace should look like this:

![](../images/projects-and-samples.png)

_**Note:** You'll see more files in your workspace, they were hidden here to make the screenshot more compact._


**Brief summary:**

* `hc-example-api-model` is a model for our API and contains one sample request `HcExampleTransformToUpperCase`.
* `hc-example-processing` contains the implementation of our API, i.e. code that handles the request, namely `HcExampleRequestProcessor`.
* `hc-example-processing-test` are tests for `hc-example-processing`.
* `hc-example-setup-debug` is the project for debugging created with `jinni setup-main`. It doesn't have any code, only dependencies (`pom.xml`) and a pointer to the installation folder of our application (file `.tribefire`).
