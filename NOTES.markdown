Overview
========

This will cover:
 * Classloading, bytecode and the JIT compiler
 * Memory Allocation, References and Garbage Collection
 * The analysis of running java programs for things like memory leaks or performance

Again this is a huge topic so further meetings may be required.

Class Loaders
-------------

### Static Linking

This requires knowing exactly where the method to call is, and can be specific to the current system and architecture.
The original way to install things on linux was:

```
configure
make
make install
```

This was because it needed to link against the files on the system.

Package management allowed this to be sustainable by providing the static link destination as a dependency.
It was still architecture specific.

### Ask for Directions

Class Loaders are a way to resolve classes in an extensible way.
You ask for the full class name and you get back the bytecode for that class.

You can use any capability of Java to calculate the bytecode:
 * Reading files
 * Making web requests
 * Performing arbitrary calculations

Class Loaders can (and do) vary by OS, so the way that the classes are resolved can be platform specific while the Java code remains independent.

By creating a custom class loader you can:
 * Create a plugin system
 * Mutate classes before loading them

### Heirarchy

A class loaded by a class loader can reference other classes. Those other classes will be loaded by the same class loader.

A normal class loader will ask it's parent to load the class first.
This behaviour is under your control. Changing it is risky - make sure you can load standard classes safely at the very least.

Normally the search only goes up. To use your class loader you must manually trigger it.
