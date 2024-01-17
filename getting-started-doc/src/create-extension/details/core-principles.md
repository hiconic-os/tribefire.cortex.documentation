# Core Hiconic Principles

Core principles of `Hiconic` are **modeling** and **modularity**.

## What is a model?

* Model is a collection of types which describe a certain domain. It consists of entity and enum types.
* Enum type defines a finite set of known values (enumeration). E.g. `DayOfWeek` with 7 values `Monday`, `Tuesday`, ... `Sunday`.
* Entity type is a type with a list of properties, and each property has a name and a type. For example a `Book` would have a `String` (text) property called `title`, and `author` of type `Witer` (another entity type).

```java
public interface Book extends GenericEntity {
    EntitType<Book> T = EntityTypes.T(Book.class);

    String getTitle();
    void setTitle(String title);

    Writer getAuthor();
    void setAuthor(Writer writer);
}
```

But modeling **data** (e.g. `Book`) is common practice. `Hiconic` models many other things, we'll focus on its **configuration** and **APIs** for now.

## Modeling Configuration

* For start, each functional component is modeled by an entity type, which we refer to as its `denotation type`.
* For example a `DatabaseConnection` with properties for `username`, `password`, `URL` and `JDBC driver`.
* All such components are stored in a special database called `cortex`.
* When starting the server, the components are read from `cortex` and "deployed". E.g. an actual `JDBC` connection would be established for each `DatabaseConnection` instance.
* Configuring a new `DatabaseConnection` is thus a matter of adding an instance of its denotation type to `cortex`.

> NOTE: Entity types that represent functional components derive from `Deployable` (and we also call them `deployables`). We also use a naming convention for a model with such types: `xyz-deployment-model`.

Example:

```java
public interface DatabaseConnection extends Deployable {
    EntitType<DatabaseConnection> T = EntityTypes.T(DatabaseConnection.class);

    String getUsername();
    void setUsername(String username);

    // and so on ...
}
```

## Modeling APIs

See the next chapter about `ServiceProcessors`. This also serves as a general example for adding a new `Deployable` type.