# Setup Platform - Tutorial Introduction

Open `devrock-sdk/env/explorer-experience/commands/setup-main.yaml`:
```yaml
!com.braintribe.model.platform.setup.api.SetupLocalTomcatPlatform {
	setupDependency: "<your-dependency>",
	installationPath: "${config.base}/../tf-setups/main",
}
```

Set the `setupDependency` property to `tribefire.setup.classic:standard-setup#3.0`:

```yaml
!com.braintribe.model.platform.setup.api.SetupLocalTomcatPlatform {
	setupDependency: "tribefire.setup.classic:standard-setup#3.0",
	installationPath: "${config.base}/../tf-setups/main",
}
```

Go to the command line, navigate to `devrock-sdk/env/explorer-experience/tf-setups` and run:

```cli
jinni setup-main
```

The command resolves the setup dependencies and builds a Tomcat based platform. In this example the `standard-setup` was used as the terminal dependency. It brings foundational services and a web-UI which we will use in this tutorial later. The resolved platform is placed under `devrock-sdk/env/explorer-experience/tf-setups/main`.
