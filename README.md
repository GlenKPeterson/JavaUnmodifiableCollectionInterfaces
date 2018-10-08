# Java™ Unmodifiable Collection Interfaces

## What
A Java™ Specification Request to make the existing Java collections interfaces extend unmodifiable interfaces with 100% backward compatibility.  java.util.Collections already has methods that return unmodifiable wrappers:

 - unmodifiableCollection(Collection<? extends T> c)
 - unmodifiableList(List<? extends T> list)
 - unmodifiableMap(Map<? extends K,? extends V> m)
 - unmodifiableNavigableMap(NavigableMap<K,? extends V> m)
 - unmodifiableNavigableSet(NavigableSet<T> s)
 - unmodifiableSet(Set<? extends T> s)
 - unmodifiableSortedMap(SortedMap<K,? extends V> m)
 - unmodifiableSortedSet(SortedSet<T> s)

This project creates interfaces that match the returned types (all modification methods removed).

## Why

 - Declaring an unmodifiable interface as a parameter to a function indicates that the function will not try to modify the collection.
 - Declaring an unmodifiable interface return type indicates that the collection should not (possibly cannot) be modified.
 - Using an interface should have the same effect as the unmodifiable wrapper, but without the wrapper (Doing noting is always faster, and takes less memory than doing something).
 - It prevents accidental modification (a source of bugs)
 - It ensures safe sharing of collections without the need for copying data (e.g. across threads)
 - It provides an extension point for immutable collections, either in Java, or in other JVM languages.

## How

Code will follow, but essentially, imagine a copy of each of the following interfaces:
 - Iterator
 - Collection
 - Map
 - Set
 - List
 - SortedMap
 - SortedSet
 
 Now imagine them with all modification methods removed, and the name prefixed with Unmod.  Like UnmodIterator would be the same as Iterator, but without the `.remove()` method.
 
 Finally, imagine the original interface now extends the Unmod interface to add the modification methods.  So Iterator extends UnmodIterator and adds the `.remove()` method.

## Trademarks
Oracle and Java are registered trademarks of Oracle and/or its affiliates. Other names may be trademarks of their respective owners.  This project is a proposed change to Java, but it is NOT Java (yet).
