# The Liskov Substitution Principle
#SOLID

## What is a type?
Type is just a bag of operations (you don't need to wonder how it really works, but how it operates)

So the definition of a type is basically the same as definition of a class. Because a class is a collection of methods and the data within is private.

## Subtype
Barbara Liskov came up with the definition of subtypes.

If we have a type `U` that can use type `T` in some way, then type `S` is a subtype of `T` if all instance of `U` can use type `S` the same as type `T`.

Subtype is always substitutable for its parent

## Duck typing
in a dynamically typed language if you want to call a method you really are sending a message to an object, the compiler doesn't know the type of that object, so the compiler has to wait until runtime to determine whether or not you can call that method (or send the message)

If the object can respond to that message the method is invoked, otherwise runtime error occurs. Here we don't need inheritance. As long as two objects respond to the same message they can be used polymorphically.


## Example
Let's say we have a class `Rectangle` to is being used by some Program

```java
public class Rectangle {
	private double height;
	private double width;
	private Point topLeft;

	public double area();
	public double perimeter();

	public double getHeight();
	public double getWidth();

	public void setHeight(double height);
	public void setWidth(double width);
}

```


We have a class that has width, height attributes, getters and setters for it, Top Left point attribute, and methods to calculate are and perimeter

Now we want to add new requirements for a `Square`. Now clearly `Square` is rectangle, so `Square` is a subtype of `Rectangle`

Now we have a problem, because as `Square` will inherit from `Rectangle` it will inherit `height` and `width` so it's going to be too large (both will be the same). Also it will inherit the setters for width and height (and it should only have one - something like `setSide`)

To solve this we will have override each of the setter methods to act as `setSide` method

```java
public class Square : Rectangle {
	public void setHeight(double height) {
		super.setHeight(height);
		super.setWeight(height);	
	}

	public void setWidth(double width) {
		setHeight(width);
	}
}
```


BUT - if some module is setting a width on (what it believes is a Rectangle) it shouldn't expect to change height as well. It can lead to undefined behavior.

### Solution 
The perfect solution is to ditch the inheritance. So treat Rectangle and Square as unrelated types. So while a square is a rectangle and a square is a subtype of a rectangle. That isn't necessarily true for the representations of both Square and Rectangle in our code

### The Representative Rule
Representatives do not share the relationships of the things they represent.


## Numbers

Integers are subtypes of Real numbers
Also every real number is a complex number.

## List
if `S` is a subtype of `T` a list of `S` is not a subtype of a list of `T`

So if we have `Circle` class that is a subtype of `Shape`. We create a List of `Circle`. It turns out we cannot pass that list to a function that expect a list of `Shape`

Why not?

Because that function could put a `Square` in the list

It can be generalized further:

Given that `S` is a subtype of `T` a generic class `P` of `S` is not automatically a subtype of the generic class `P` of `T`

## Heuristics

- If the base class does something, the derived class must do it too, and it must do it in a way that does not violate the expectation of the callers. 
This means that you cannot take expected behaviors away from a subtype. Subtype can do more than its parent type - but it can never do less. 

Whenever you have a derived class that has degenerate functions in it (functions that don't do anything). Than you've possible got a LSP violation, especially if those functions were implemented in the base class. This is not a hard rule!

More obvious clue is when a derived function is written to unconditionally throw an exception. This is clearly a violation of LSP as the author doesn't want anyone to call this function


## The modem problem

Consider a system in which a very old suite of programs called the file movers move files around the network using modems

So we have `FileMover`  main Program that uses abstract interface `Modem<I>` that is an abstraction for different types of modems

`Modem` interface has methods like `Dial`, `Hangup`, `Send`, and `Receive` - But new requirement has been added - to include model that don't need to be dialed. They are permanently connected. So we have `DedModem` (Dedicated Modem) class that has only `Send` and `Receive` methods.

The easiest thing to make it work is to derive `DedModem` from the `Modem` interface. But for that to work we will have to create empty `Dial` and `Receive` methods that do nothing.

But this is a change in behavior! The class `FileMovers` doesn't know that those function do nothing and may base its behavior on the assumption that it does. It can lead to weird functionality

Clearly LSP violation. and we have complicated system for both Dedicated modem users in application and for `FileMover` class. 

The possible solution is to use Adapter that is an abstraction connecting `Modem` interface and `DedModem` class