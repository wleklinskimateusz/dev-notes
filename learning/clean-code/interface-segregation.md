# The Interface Segregation Principle

#SOLID

>don't depend on the things you don't need ~ the Interface Segregation Principle

Imagine having very simple system: system that turns on the light based on a switch position.

The simplest system that solves this is a `Switch` class that is depending on `Light` class.

```java
public class Switch {
 private Light light;

 public Switch(Light light) {
  this.light = light;
 }

 public void activate() {
  light.turnOn();
 }
}
```

BUT Switch now has an attribute called `light` and the switch shouldn't know anything about the light,
because it could control anything. To fix this we need to create an interface between the `Switch` and the `Light`.
The interface would have to have `turnOn` method, the Light will implement the interface,
and the light will supply the implementation for the `turnOn`method.

We may think that this interface we created is strongly connected to the light.
But light doesn't need that interface to operate - the `Switch` class does!. So it is strongly connected to the `Switch`.

If we would take the switch into separate package with the interface,
and the light in the separate one, the `Light` can become a plugin to the `Switch` class.
We can also create other classes like `TV`, `Blender`, `Fan` 
all which implement our interface and those could be independent plugins as well.

>Q: What should we name this interface
>A: maybe... `Switchable`! great name ;D

***Interfaces have more to do with the classes that use them, that with the classes that implement them***

## What is an interface?

Interface is an abstract class with nothing but abstract methods in it.

In java we have `interface` syntax only because classes cannot have more then one base class 
(and can implement more than one interface)

## The Job class

Imagine we have a huge system that highly depend on the class `Job` (for handling printers)
A lot of modules depend on that class, so whenever anything changes inside `Job`
each of the modules had to be recompiled. 
To solve this we could create a bunch of interfaces that group similar functionalities and communicate with subsystems independently.

## Fat classes

If we have really big, important and hard to split class, we can use this technique (ISP).

One may argue, that compile times aren't that big of an issue, to be concern with this.
And this is a good point, but the ISP also solves another problem. 
It decouples the systems so that each of the modules can be plugins to the main and all can be easily split into small chunks.

When components can be deployed separately that means that they can also be developed separately. 
So this can be more efficient as programmers won't interfere with each other
