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

### Security

A class that is loaded may not be trustworthy. Answers generated from stack overflow could be wrong.

The capabilities of a class that has been loaded can be restricted by the loader.
This uses the Java Security Model.
You can define a custom set of permissions that apply to your classes.

This can prevent malicious code from doing things like reading or writing files or creating network connections.
(Outside current presentation scope to cover the Java Security Model).

This is how Applets work.

Bytecode
--------

Bytecode is the binary representation of Java code.
It is still an interpreted language. It is interpreted by the JVM.

### Not Scary

It works like assembly using instructions and registers. Registers are stacks.

Instructions fall into a number of broad groups:

 * Load and store (e.g. aload_0, istore)
 * Arithmetic and logic (e.g. ladd, fcmpl)
 * Type conversion (e.g. i2b, d2i)
 * Object creation and manipulation (new, putfield)
 * Operand stack management (e.g. swap, dup2)
 * Control transfer (e.g. ifeq, goto)
 * Method invocation and return (e.g. invokespecial, areturn)

There are also a few instructions for a number of more specialized tasks such as exception throwing, synchronization, etc.

There are different operations for the different primitive types. E.G. int / long / float etc.
