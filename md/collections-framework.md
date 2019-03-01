# Collections Framework


-
-
## The Collection Interface

|||
| -------------------- | --------------------------------- |
| `add(E)`             | `addAll(Collection<? Extends E>)` |
| `remove(o)`          | `removeAll(Collection<?>)`        |
| `clear()`            | `removeIf(Predicate<? super E>)`  |
| `size()`             | `containsAll(Collection<?>)`      |
| `stream()`           | `iterator()`                      |
| `isEmpty()`          | `contains(Object)`                |
| `toArray()`          | `T[] toArray(T[])`                |
|||



-
-
### Collections and Maps

||||
| ---------- | ------------- | --------------- |
| ArrayList  | EnumSet       | EnumMap         |
| LinkedList | LinkedHashSet | LinkedHashMap   |
| ArrayDeque | PriorityQueue | WeakHashMap     |
| HashSet    | HashMap       | IdentityHashMap |
| TreeSet    | TreeMap       |                 |
||||

Note: `WeakHashMap` uses `WeakReference` objects as keys; can be GC'd if no other references remain
`IdentityHashMap` uses `System.identityHashCode()` and `==` for storage and retrieval

-
-
## Collections vs Maps

Collections hold a series of individual elements.  
Maps store associated pairs of objects (called key-value pairs). The key object is used to look up the value object. Sometimes called dictionaries or associative arrays.  
Both resize automatically (unlike Arrays).


-
### List types

- ArrayList - Quicker with random access to elements
- LinkedList - Quicker with removal/insertion of elements in the middle of the list

-
### Set types

- HashSet - keeps elements in hash order (fast, not predictable)
- TreeSet - keeps elements in ascending sorted order
- LinkedHashSet - provides insertion-order access to elements
- BitSet - Optimized for storing sequences of bits
- EnumSet - Optimized set for holding `enum` instances

Sets are often used to test for membership using the `contains()` method

-
### Queues, Dequeues, and Stacks

- Queue -- Adds elements to one end and removes from the other (FIFO)
- Stack -- Adds elements to one end and removes them from the same (LIFO)
- Dequeue -- "double-ended queue" adds and removes elements at both ends

Note: `Dequeue` is often used for stacks as well

-
-
## Map

A Map is an object that associates keys to values.

### Example:
  - phonebook
  - dictionaries

-
## Map

#### Phonebook

| Name(key) | Number(value) |
|------|--------|
|Wilhem|111-111-1111|
|Dolio|222-222-2222|
|Froilan| 333-333-3333|

-

## Map

- Elements/Entries are pairs of objects, called keys and values
- Keys are used to lookup values
- Keys are unique
- Values does not have to be unique
- Key has to be associated with a value (null can be a value)

-
## Map

Create a map

```
//creating a hashmap
Map<String, String> phonebook = new HashMap<String, String>();

//creating a treemap
Map<String, String> phonebook = new TreeMap<String, String>();
```

-
## Map

Add entries `put(key, value)`

```
Map<String, String> phonebook = new HashMap<String, String>();
//phonebook.put(key, value)
phonebook.put("Wilhem", "111-111-1111");
phonebook.put("Dolio", "222-222-2222");
phonebook.put("Froilan", "333-333-3333");
```

| Name(key) | Number(value) |
|------|--------|
|Wilhem|111-111-1111|
|Dolio|222-222-2222|
|Froilan| 333-333-3333|

-
## Map
`.get(key)`

Given a key, give me the value associated with it

```
phonebook.get("Wilhem"); //"111-111-1111"
phonebook.get("Dolio"); //"222-222-2222"
phonebook.get("Kris"); //null
```

| Name | Number |
|------|--------|
|Wilhem|111-111-1111|
|Dolio|222-222-2222|
|Froilan| 333-333-3333|

-
## Map
`.getOrDefault(key, defaultValue)` (Java 8+)

Given a key, give me the value associated with it.

If there is no value, then return the default value.

```
phonebook.getOrDefault("Wilhem", ""); //"111-111-1111"
phonebook.getOrDefault("Kris", ""); //""
```

-
## Map

Update entries `.put(key, value)`

```java
phonebook.put("Wilhem", "111-111-1111");

// updating the value for Wilhem
phonebook.put("Wilhem", "444-444-4444");
```

| Name(key) | Number(value) |
|------|--------|
|Wilhem|444-444-4444|

-
## Map - Keys

Get all the keys `.keySet()`

```java
Map<String, String> phonebook = new HashMap<String, String>();
phonebook.put("Wilhem", "111-111-1111");
phonebook.put("Dolio", "222-222-2222");
phonebook.put("Froilan", "333-333-3333");

//get all the keys
Set<String> allKeys = phonebook.keySet();

```
-
## Map - Values

Get all the values `.values`

```java
Map<String, String> phonebook = new HashMap<String, String>();
phonebook.put("Wilhem", "111-111-1111");
phonebook.put("Dolio", "222-222-2222");
phonebook.put("Froilan", "333-333-3333");

//get all the values
Collection<String> allValues = phonebook.values();

```

-
## Map - Entries

Get all the entries `.entrySet()`

```java
Map<String, String> phonebook = new HashMap<String, String>();
phonebook.put("Wilhem", "111-111-1111");
phonebook.put("Dolio", "222-222-2222");
phonebook.put("Froilan", "333-333-3333");

//get all the entries
Set<Map.Entry<String, String>> entries = phonebook.entrySet();

```

-
# Map

- `size()` - the number of elements in the map
- `get(key)` - get the value associated with the key
- `put(key, value)` - add the key and value to the map
- `remove(key)` - remove the entry with this key
- `containsKey(key)` - returns true if it has the key
- `containsValue(value)` - return true if it has the value
- `entrySet()` - return all the elements in the map
- `isEmpty()` - return true if size is 0
- `keySet()` - return all the keys
- `values` - return all the values

[Java Map API](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)

-

## Map types

- `TreeMap` - Keeps keys in insertion order
- `HashMap` - Hashes keys for quick access
- `ConcurrentHashMap` - similar to HashMap but can be use concurrently

-
## Map

### Resources
- Core Java 9.3
- [Java Trail - Map](https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html)
- [dummies - Map](https://www.dummies.com/programming/java/what-is-a-java-map/)
- [Java Map API](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)
- [Java HashMap API](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
- [Java TreeMap API](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)
- [Java ConcurrentHashMap API](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)
- [Nhu - How to use a Map](https://medium.com/@nhu313/how-to-use-a-java-hashmap-2df489f482aa)
- [Nhu - What is a HashMap](https://medium.com/@nhu313/what-is-a-java-hashmap-83152fb632bb)

-
-
## Collections Framework Part 2

-
-
## Iterators

Provides a way to iterate through a Collection.  
Implicitly used in foreach loops.  
Methods:

- `hasNext()` - returns true if there are more elements available
- `next()` - return the next element
- `remove()` - remove the last element returned from the underlying Collection

-
## ListIterators

Slightly more features than Iterators:

- Can iterate backward
- Provides index for previous and next elements


-
-
## Views

- Lightweight collection implementations
- No storage functionality
- Produce subset, empty, singleton, or unmodifiable Collections

-
-
## Utility Classes

- [Collections](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html)
- [Arrays](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html)
