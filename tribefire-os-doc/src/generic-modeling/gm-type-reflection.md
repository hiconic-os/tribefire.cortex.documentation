# Generic Model Type Reflection

Generic Model Type Reflection (`GMTR`) is the feature that makes generic data processing easy with `GM`.

Let's get the gist of what this reflection is with a simple example.

## Example

### Entity Declaration

Consider this entity:

```java
public interface Book extends GenericEntity {
	EntityType<BookA> T = EntityTypes.T(Book.class);

	String getTitle();
	void setTitle(String title);

	String getAuthor();
	void setAuthor(String author);

	String getIsbn();
	void setIsbn(String isbn);

	int getNumberOfPages();
	void setNumberOfPages(int numberOfPages);

	Date getYearPublished();
	void setYearPublished(Date yearPublished);
}
```

### Example task

Imagine, we want to simply print its type and the name and a value for each of it's properties.

Expressive code would look like this:

```java
public void print(Book book) {
    System.out.println("Book: ");
    System.out.println("title: " + book.getTitle());
    System.out.println("author: " + book.getAuthor());
    System.out.println("isbn: " + book.getIsbn());
    System.out.println("numberOfPages: " + book.getNumberOfPages());
    System.out.println("yearPublished: " + book.getYearPublished());
}
```

Now, let's write a generic code (one that doesn't even know that `Book` exists) to achieve the same result:

```java
public void print(GenericEntity entity) {
    EntityType<?> type = entity.entityType();
    System.out.println(type.getShortName + ": ");

    for (Property p: type.getProperties())
        System.out.println(p.getName() +  ": " + p.get(entity));
}
```

### Explanation

We have seen `EntityType<?>` before, because it is the type we need to even instantiate an entity with `EntityType.create()` method.

This example shows us:
* entity can tell us its type via its `GenericEntity.entityType()` method (analogous to `Java`'s `Object.getClass()`
* `EntityType<?>` knows about all it's properties
* `Property` object knows its name and can be used to read a property value of an `entity`

### Minor correction

The two examples are actually not equivalent. We have not seen that yet, but `GenericEntity` has 3 properties (`id`, `globalId` and `partition`), which every entity inherits, and this code would print those too. To avoid it, we could for example ignore properties declared on GenericEntity:

```java
public void print(GenericEntity entity) {
    EntityType<?> et = entity.entityType();
    System.out.println(et.getShortName + ": ");

    for (Property p: et.getProperties())
        if (p.getFirstDeclaringType() != GenericEntity.T)
            System.out.println(p.getName() +  ": " + p.get(entity));
}
```


