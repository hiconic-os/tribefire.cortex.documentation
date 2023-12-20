# Generic Modeling (GM)

`GM` is a paradigm extending a programming language with support for data-types.

## Motivation

**Generic data processing** is **nothing new**, with common examples being **serialization as JSON or XML**, or **mapping data to an SQL Database** (say with `Hibernate`). However, if you **try to implement** a similar feature in a generic way, you realize how **utterly tedious** it is using `Java reflection` with `Classes` and `Methods`. The core of the problem is that languages like `Java` **miss dedicated types to represent data**. Instead, they are focusing on functional code and data types are just functional classes with no functionality.

Also, with **generic processing** you often realize you **need features your objects don't have**. For example, when querying an entity from a DB, and the entity references another entity, you might not want to load the second entity right away, but only if and when it's accessed. Such a feature (lazy loading) is still doable, but quite more complicated.

 `GM` is addressing both of these issues and more. It extends the language with additional type-system designed for data, with powerful features beyond just storing values, and with tools to make common generic tasks easy.

## Core GM

Following articles describe the core of `GM` - it's type system with its features:

**[Models and GM types](models-and-gm-types.md)** introduces `models` as a collection of custom `GM` types and shows how to declare these types in `Java`.

**[GM Type Reflection](gm-type-reflection.md)** shows how `GM` data can be manipulated in a generic way.

**[Advanced Entity Features](advanced-entity-features.md)** shows extra features of `GM` types beyond the basic reflection use-cases.

## Notable Models

As advertised, `GM` is a technology consequently built on models. Here are the most important core models:

**[Meta Model](notable-models/meta-model.md)** - a model that describes other models.

**[Meta Data Model](notable-models/meta-data-model.md)** - a model that brings additional information to a model, beyond the pure type information.

**[Resource Model](notable-models/resource-model.md)** - a model for representing unstructured (binary) data.

**[Reason Model](notable-models/reason-model.md)** - a model for communicating errors, problems, exceptions, ...

**[Service Api Model](notable-models/service-api-model.md)** - a model for describing functional APIs


* **Model** s a collection of entity and enum types describing a certain domain.
* **Entity Type** is a type that has a name and a list of properties, where each has a name and a type. (e.g. Person has a name of type String and a birthDate of type Date).
* **  **  

NOTE that:
* this technology is usable and useful on its own, without `Tribefire` platform.
* this technology is language agnostic. Our main target platform is `Java`, with secondary support in `JavaScript`, but the paradigm can be integrated into any language.