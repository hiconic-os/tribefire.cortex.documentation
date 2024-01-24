# Service Processing

## Service Processors

`ServiceProcessor` is a `Deployable` that represents an API which returns a response for some request. Each request is modeled by an entity type of course.

> IMPORTANT: We will now discuss how to add a new `ServiceProcessor` to _Hiconic_. Note that this doesn't have to be done manually, next article describes how to create all the artifacts and a sample code with `jinni` CLI tool.

To add a new `ServiceProcessor` to _Hiconic_ we need to:
* Model the **request hierarchy**. Typically would would have an abstract type `XyzRequest` and concrete sub-types e.g. `ReadXyzStuff` or `StartXyzProcess`. Artifact: `xyz-api-model`
* Create an **actual implementation**, usually called `XyzRequestProcessor` which extends the interface `ServiceProcessor<?, ?>`. Artifact: `xyz-processing`.
* Model a **denotation type** called `XyzServiceProcessor` which extends the denotation type `ServiceProcessor` (which extends `Deployable`). Artifact: `xyz-deployment-model`.
* **Bind the implementation to it's denotation**, i.e. tell _Hiconic_ how to instantiate and parameterize an implementation based on a denotation instance. Artifact: `xyz-module`

> NOTE: There are two different `ServiceProcessor`s mentioned, one is an **expert interface**, and one is an **entity type**. It is common in _Hiconic_ to give a denotation type the name of the expert interface it models.

## Service Domains

With the above steps we can create new instances of our processor and _Hiconic_ knows how to deploy them. But just a deployed processor is not enough, we can't even call it. We need to define a `ServiceDomain` - a logical space which contains request types and defines which processor handles which request.

So in order to make our processor accessible we need to add this configuration to `cortex`:
* Create a new `ServiceDomain` with a human-readable name `Xyz Service Domain` and a technical identifier `xyz`.
* Create a new configuration model `configured-xyz-api-model` which depends on our `xyz-api-model`.
* Configure `ProcessWith` metadata on `XyzRequest`, specifying the processor is `XyzServiceProcessor`.

All this would be done in an `xyz-initializer`.

That's it. Now we have an `xyz` service domain, and can evaluate our `XyzRequest`s against it.

As mentioned above, all this code can be created with our CLI tool `Jinni`.