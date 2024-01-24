# All Extension Artifacts

For good measure, let's review one more time the files we see here, from top to bottom.

Note that a sample request was created which simply transforms given text to uppercase.

**hc-example-api-model** contains the abstract `HcExampleServiceRequest` and a concrete `HcExampleTransformToUpperCase` request.

**hc-example-deployment-model** contains a denotation type `HcExampleServiceProcessor` for our expert.

**hc-example-initializer** contains, besides standard initializer classes, a `HcExampleServiceDomainSpace`. Here the entities representing our `ServiceDomain` with a `ServiceProcessor` and a properly configured model are defined.

Q: How does the initialization work?
A: When starting the server, all initializers are run and generate data for every `Collaborative Smood Access`, such as `cortex`. The process calls the `HcExampleInitializerSpace.initializer()` method, which in our sample looks like this:
```java
@Override
public void initialize() {
	HcExampleServiceDomain.serviceDomain();
}
```
This thus triggers our `HcExampleServiceDomainSpace.serviceDomain()` method which than leads to invocation of all the other methods in that class. Every time we call `create()` with an entity type as parameter, such as `create(ServiceDomain.T)`, a new instance is created inside our access.

BTW we specify this initializer targets `cortex` in its `asset.man` file:

```gmml
$nature = !com.braintribe.model.asset.natures.PrimingModule()
.accessIds = ('cortex')
```

**hc-example-module** contains `HcExampleModuleSpace` which binds our denotation type `HcExampleServiceProcessor` to its expert implementation `HcExampleRequestProcessor`.

The binding code:
```java
@Override
public void bindDeployables(DenotationBindingBuilder bindings) {
    bindings.bind(HcExampleServiceProcessor.T) //
            .component(tfPlatform.binders().serviceProcessor()) //
            .expertSupplier(this::HcExampleRequestProcessor);
}
```
**hc-example-processing-test** is self-explanatory. It contains a sample test for our convert-to-uppercase processor.

**hc-example-processing** contains the expert for evaluation of `HcExampleServiceRequest`. Note the implementation derives from `AbstractDispatchingServiceProcessor`, which provides a convenient way to simply map requests to corresponding handler methods:
```java
@Override
protected void configureDispatching(DispatchConfiguration<HcExampleServiceRequest, Object> dispatching) {
		dispatching.registerReasoned(HcExampleTransformToUpperCase.T, (c, r) -> transformToUpperCase(r));
}

private Maybe<String> transformToUpperCase(HcExampleTransformToUpperCase request) {
	String text = request.getText();

	if (text == null || text.isEmpty())
		// NOTE this is obviously not reasonable, it's just here to demonstrate error handling with Maybe and Reasons (InvalidArgument)
		return InvalidArgument.create("Cannot convert null or empty text to uppercase.").asMaybe();

	return Maybe.complete(text.toUpperCase());
}
```

> NOTE we use `registerReasend` which forces our handler method to return `Maybe<String>` rather than directly `String`. This is highly recommended as it brings native error-handling to the (request processing) protocol.

**hc-example-setup-debug** is the project that was created with `jinni setup-main`. It reflects the `hc-example-setup` artifact and references the _Hiconic_ platform as well as all the modules and initializers. This project is run by the `Tomcat` plugin in order to debug our application.

**hc-example-setup** as the name suggests, defines our entire application, including the _Hiconic_ platform, modules, initializers, front-end application (in our case `tribefire-explorer`) and everything else.

When `Jinni` performs a setup, it collects all the assets and process each of them specifically, based on their so called nature.

Note that for now, `Jinni` is not extensible, so only well-known assets are supported.

This setup project's nature is an `AssetAggregator` (as defined in its `asset.man`), which means it's aggregating a bunch of assets via `pom.xml` dependencies.


