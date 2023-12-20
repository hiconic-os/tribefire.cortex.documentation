# Models and Gm Types

`Model`, for our purposes, is a collection of types that describe object from a certain domain. Let's use an example.

## Example

Imagine we deal with **pet animals**, for now limited to **dogs** and **cats**.

For each animal we want know its `name` and `birth date`, and for dogs we also want to know what's the `dog's breed`.

In `GM` we'd create a model artifact called `animal-model`, with an abstract type `Animal` and two concrete (instantiable) sub-types `Dog` and `Cat`.

### With model grammar

This model thus contains three `entity types` and an `enum type`. In some pseudo language it would look like this:

```java
abstract entity Animal {
	name: string
	birthDate: Date
}

entity Dog extends Animal {
	// Dog is an animal, but has an additional property - its breed
	breed: DogBreed
}

entity Cat extends Animal {
	// Cats have nothing extra
}

enum DogBreed {
	labrador,
	goldenRetriever,
	husky,
	// and others
}
```

### With Java interfaces

Ideally, we'll one day build a grammar and support for such a concise notation. We're stuck with `Java` for now though. Behold:

WARNING: this might be a little confusing if you're not used to it.


```java
// NOTE: each interface/enum would of course be a separate file and packages and impirts were left out for readability

@Abstract
public interface Animal extends GenericEntity {
	EntityType<Animal> T = EntityTypes.T(Animal.class);

	String getName();
	void setName(String name);

	Date getBirthDate();
	void setBirthDate(Date birthDate);
}

public interface Dog extends Animal {
	EntityType<Dog> T = EntityTypes.T(Dog.class);

	DogBreed getBreed();
	void setBreed(DogBreed breed);
}

public enum DogBreed implements EnumBase {
	labrador,
	goldenRetriever,
	husky,
	// and others
	;

	public static final EnumType T = EnumTypes.T(DogBreed.class);

	@Override
	public EnumType type() {
		return T;
	}
}

public interface Cat extends Animal {
	EntityType<Cat> T = EntityTypes.T(Cat.class);
}
```

### Explaining the interfaces

OK, the `Java` example looks a little ~rough~ technical and raises some questions. Let's address them one by one:

**Q:** What's `GenericEntity`?
**A:** `GenericEntity` is the common super-type of all entities, just like `Object` is the common super-type of all `classes` in `Java`, even if not declared as a super-class explicitly. But we have to declare the super-type explicitly to be able to assign any entity instance to a variable of type `GenericEntity`.

**Q:** What's this: `EntityType<Animal> T = EntityTypes.T(Animal.class);`?
**A:** The `T`, which is a static final field on the interface, is what we call a type literal. It's the equivalent of `Something.class` class literal. The right hand side is the `GM` magic that creates the value for `T`, thus making these entities work.

**Q:** So the `T` field is of type `EntityType<Animal>`?
**A:** Yes. `EntityType` is the reflection object for entities, similar to how `Class` is a reflection object for Java classes. And `Animal.T` is of type `EntityType<Animal>`, just like `HashMap.class` is of type `Class<HashMap>`.

**Q:** Why are those entities `interfaces`?
**A:** Short answer: nothing else works. Long answer: **Don't think about it as interfaces**, this of it as entity declaration in the first example, but in a way that works in pure `Java`. If there was a native language for `GM`, these interfaces would be a `Java` emulation of the entity grammar of that language.

Interfaces work, as they allow multiple inheritance and the code is pure declaration (no implementation).

Ideally, we'd love to use the special model grammar one day, but that comes with some challenges in terms of IDE support (code completion, compile-time checking). Although there is a small disadvantage - we have no compile-time check whether the getter are setter names are matching. If not, expect an error in runtime.

**Q:** Do I have to implement these interfaces?
**A:** No, this is done automatically by the `GM` runtime environment, for which you just need `com.braintribe.gm:gm-core4-jvm` on classpath.

**Q:** How do I create an instance?
**A:** Like this:

```java
Dog dog = Dog.T.create();
dog.setName("Wolfgang");
dog.setBreed(DogBreed.husky);
```

**Q:** OK, but what's the big deal? Aside from the multiple inheritance I could have just used a POJO with a field and a getter+setter for each property. I wouldn't even have to write the getters and setter with Lombok.
**A:** Glad you asked. These entities are way more powerful than mere records for property values. Just read on...

## Next

Now that we've seen a simple model example, let's examine the modeling capabilities more in depth. 

**[Reference: Gm Type System](ref-gm-type-system.md)** describes the full modeling possibilities with `GM`.

**[GM Type Reflection](gm-type-reflection.md)** shows how entities can be manipulated generically with `GM` reflection.

**[Advanced Entity Features](advanced-entity-features.md)** shows entity features beyond simply storing property values.