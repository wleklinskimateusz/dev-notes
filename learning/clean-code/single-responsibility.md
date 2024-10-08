# The Single Responsibility Principle

#SOLID

## What is a responsibility

consider a class `Employee`

```typescript
class Employee {
 calculatePay: () => number;
 save: (details: Partial<Employee>) => void;
 describeEmployee: () => string;
}
```

Q: How many responsibilities does this class have?
 A: 3
now let's add `findById` method to this class

```typescript
class Employee {
 calculatePay: () => number;
 save: (details: Partial<Person>) => void;
 describeEmployee: () => string;
 findById: (id: number) => Person
}
```

Q: now how many responsibilities does this class have?
A: not it is still 3, as `findById` is in the same family as `save` (database functions)

sometimes it is not as simple, and to deduct in which family a particular method lives can be decided by who is
the audience of that method (and who could potentially request changes)

## It's all about users

For example:
for the family of function that calculates pay the users requesting change would be the lawyers, managers and accountants.

For the family of function that connects to database, it would be the people that manages schema,
decides on specific database solutions etc

## It's about roles

So people or groups of people that have certain interest and may request changes in our code are called ***Actors***.

Whenever the needs of an actor will change, the family of needs of that actor will also have to change

***Responsibility is a family of functions that serves one actor***

## The two values of Software

### Behavior

if the software does what the user needs without bugs, delays or crushes, that behavior value is high

This is achieved when the current software meets the current needs of the current user

BUT - the needs of the users change, so this value tend to fade
Solution: You have introduce new features, to fit new needs of the users

### Ability for a software to change

This is more important value of software. Without it, it can't live long

If the behavior value is low, and the system is able to change quickly and cheap. Then it may be disappointing at first,
but this system can be modified to answer feedback and user are more and more satisfied

## Co-location is coupling

If we add a method to a class that handles more than one thing, all the classes that depend on that class
has to be recompiled and redeployed.

## Single Responsibility Principle

***a module should have one and only one reason to change***

In other words we gather together the things that change for the same reasons and we separate the things
that change for different reasons

## Design Flow

When designing a system we need to:

- understand who the actors are
- identify the responsibilities that serve those actors
- allocate responsibilities to modules such as each module has one and only one responsibility

## Examples

### create and send message

```java
private String assembleDirections() {
  available = new StringBuffer();
  nDirections = directions.size();
  directionsPlaced = 0;
  for (String dir : new String[]{Game.NORTH, Game.SOUTH, Game.EAST, Game.WEST}) {
   if (directions.contains(dir)) {
    placeDirections(dir);
   }
  }
  return "You can go " + available.toString() + " from here.";
}

private void placeDirection(String dir) {
 directionPlaced++;
 if (isLastOfMany())
  available.append(" and ");
 else if (notFirst())
  available.append(", ");
 available.append(directionName(dir));
}
```

The example above shows a function that create a set of direction and sends this data to the user. Those are two responsibilities

For example if the language of the direction were to change, one of the responsibilities would have to change,
and the other not.

### shoot arrow

```java
private int shootAsFarAsPossible(String direction, int cavern) {
 int nextCavern = adjacentTo(direction, cavern);
 if (nextCavern == 0)
  return cavern;
 else {
  if (nextCavern == wumpusCavern) {
   wumpusHitByArrow = true;
   gameTermintated = true;
   return nextCavern;
  } else if (nextCavern == playerCavern) {
   gameTerminated = true;
   hitByOwnArrow = true;
   return nextCavern;
  }
  return shootAsFarAsPossible(direction, nextCavern);
 }
}
```

You could think that this function has a single responsibility. This is a recursive algorithm that follows the error
and reports where it lands.
BUT
it also terminates the game. And those are two responsibilities. One is policy and the other is mechanics.
Those should live in different modules

### Logging

But what about the situation when we have a need to create logs of our program?
Clearly logging is its own responsibility, but how can we possibly separate this from the code?

The answer is, we should divide the function into multiple very small functions and ignore logging the messages for now.
When we have a base class that does all the logic, we could derive another class from this class
and to each function add a logging statement.
