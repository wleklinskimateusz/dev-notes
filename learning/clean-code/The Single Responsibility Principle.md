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

sometimes it is not as simple, and to deduct in which family a particular method lives can be decided by who is the audience of that method (and who could potentially request changes)

## It's all about users

For example:
for the family of function that calculates pay the users requesting change would be the lawyers, managers and accountants. 

For the family of function that connects to database, it would be the people that manages schema, decides on specific database solutions etc



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

If the behavior value is low, and the system is able to change quickly and cheap. Then it may be disappointing at first, but this system can be modified to answer feedback and user are more and more satisfied



