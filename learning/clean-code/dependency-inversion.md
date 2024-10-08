# The Dependency Inversion Principle

#SOLID

## What is a dependency?

Two kinds of dependencies:

- Runtime dependency
- compile-time dependency

### Runtime dependency

- When the flow of control leaves one module and enters another,
- if one module accesses the variables inside another,
- Whenever two modules interact at runtime

### Compile-time dependency (Source code dependency)

when a name is defined in one module, but it appears at another module,
then that module has a source code or compile-time dependency on the defining module.

For example in java:
there is a class `A` and a class `B` and `A` depends on `B`.
When class A is compiled the compiler must find out about the details about class `B`.
It is doing so, by looking for binary file `b.class` and if it cannot find it,
or it finds it but it is older than its source code `b.java` then it compiles that module.

So to compile one module you have to compile all the modules that that module depend upon

## Structured design

this is a top-down methodology. You start with main, and then you design the subroutines that the main should call,
and then the subroutines that those subroutines would call and so on.

That program has a source code dependencies that exactly mimic runtime dependencies of a program. (not a good idea).
With that design we have hard time keeping the dependencies from crossing team boundaries.

> We don't want the source code dependency structure to look like runtime dependency structure.

## Polymorphism

suppose we have a module named `A` that calls the function `f` on the module named `B`.
Then `A` has both compile time and runtime dependency on `B`.
But now let's make this call on `f` polymorphic by introducing the Interface
(`A` would use the interface and `B` would implement it).

Now `A` has a runtime dependency on `B` but it doesn't have a source code dependency on `B` anymore. 
Both `A`, and `B` have a source code dependency on the interface.

The source code dependency of `B` on the interface points
in the opposite direction of the runtime dependency of `A` upon `B`.

that is ***Dependency Inversion***

> Dependencies are inverted whenever the source code dependencies oppose the direction of the flow of control

## Boundaries

Whenever we want a boundary to exist we have to choose which dependency to invert against the flow of control,
so that all the dependencies points in the same direction across the boundary.

That is the way that we create ***plugins***: [[gloassary#Plugin]]

So your goal should be to divide your system with boundaries and to invert the dependencies that cross those boundaries

## Architectural implications

See formal definition of Dependency Injection: [[gloassary#Dependency Inversion Principle]]

modules that contain high-level policies, 
such as use cases, should not depend on those modules that contain low-level details, such as databases or formatting.

And yet those high level modules must eventually invoke those low level functions.
Use cases must read database records, and display web pages.

The solution to this is to invert the dependency on the boundary
that separate the use cases from the database and the web system.
So we design the system so that the database and web systems are plugins to the application.

## A reusable framework

When you want to build reusable framework, 
try to build it in parallel because you can't know from the single example what can be reused and what cannot.
