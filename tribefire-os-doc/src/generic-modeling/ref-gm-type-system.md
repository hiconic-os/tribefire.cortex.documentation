# Reference: Gm Type System


## Vocabulary

`Type Signature` is the name that uniquely identifies a type, similar to a class name in Java.

`GM Type` is any type in the `GM` Type System. `String` is a (custom) GM type, `Visible` (meta-data) is a GM type (Entity Type), but `java.lang.StringBuilder` is not a GM type.

`GM Value` is a value who's type is a `GM Type`. The `String` 'Hi there', an integer 420 or an entity are all GM values.

`Custom Type` is either an `Entity Type` or an `Enum Type`.

## Types

### Simple types

`GM` supports 8 simple types:

Type Signature | Nullable Java type | Non-Nullable Java Type | Note
------- | ----------- | ----------- | ----------- 
integer | Integer | int | 32-bit signed integer
long | Long | long | 64-bit signed integer
float | Float | float | 32-bit floating point number
double | Doule | double | 64-bit floating point number
boolean |Booelan  | boolean | true/false
string | String | - | text
date | Date | - | java.util.Date
decimal | BigDecimal | - | java.math.BigDecimal


### Collections

`GM` supports 3 collection types:

Type Signature | Java type
------- | ----------- 
list<E> | java.util.List<E>
set<E> | java.util.Set<E>
map<K, V> | java.util.Map<K, V>

Note that a collection element type cannot be a collection. Even if the declared type of the element is [Object (base type)](#base-type), the value must not be a collection.


### Enum Type

`Enum type` has a custom type signature and a list of constants, just like a `Java` enum.

In `Java` it must also implement the `EnumBase` interface, which marks it as part of the model, because there could be enums used for other reasons, which are not part of the model. Also, it makes generic algorithms more elegant, e.g. when determining the type of a value.

#### Enum Type Example

type signature: `com.mycompany.Color`

```java
package com.mycompany;

public enum Color implements EnumBase {
	red,
	green,
	blue
	;

	public static final EnumType T = EnumTypes.T(Color.class);

	@Override
	public EnumType type() {
		return T;
	}
}
```

### Entity Type

`Entity type` has a custom type signature and a list of properties, each of which has a name and a type, which must be a `GM type`.

#### Entity Type Example:

type signature: `com.mycompany.JackOfAllTrades`

```java
package com.mycompany;

public interface JackOfAllTrades extends GenericEntity {
	EntityType<Animal> T = EntityTypes.T(Animal.class);

    #Mandatory
	String getString();
	void setString(String string);

	Date getDate();
	void setDate(Date date);

	int getNonNullableInt();
	void setNonNullableInt(int nonNulableInt);

	Integer getNullableInt();
	void setNullableInt(Integer nulableInt);

	JackOfAllTrades getJackOfAllTrades();
	void setJackOfAllTrades(JackOfAllTrades jackOfAllTrades);

	List<String> getListOfString();
	void setListOfString(List<String> listOfStrings);

	Color getColor();
	void setColor(Color color);

	Object getObject();
	void setObject(Object object);
}
```

### Base Type

type signature: `base`
Java type: `Object`

`Base type` is special - it can only be a type of a property (`Object` in `Java`), but no value ever has this type. The point to let these properties have values of different, mutually-incompatible types (e.g. `GenericEntity.id` is of `base` type, as we wish to support `String` and `Long` (and even others) as possible id types for every entity).


## Relationship to Models

Typically, every `Custom type` is defined in some model artifact, and every model except for one is a collection of collection of `Custom types`.

The sole exception is `com.braintribe.gm:root-model`, which besides `GenericEntity` also contains `Base type` and the 8 `Simple types`. 

It is possible to declare `Custom types` outside of model artifact, but this should be limited to cases where such entities are used internally in some artifact, thus extracting them to a standalone model artifact would be extra effort with no added value.

`Collection types` do not belong to any model.

Thus, except for `Custom types` used internally and `Collection types`, every `GM type` belongs to exactly one model.