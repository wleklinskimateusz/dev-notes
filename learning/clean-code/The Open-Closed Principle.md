# The Open-Closed Principle
#SOLID

***Software module should be open for extension, but closed for modification.***

Open for extension - it should be very simple to change behavior of that module
Closed for modification - the source code shouldn't change

We can accomplish that by creating an abstract interface and separate details from the actual module

## Example

Imagine we have a method

```java
void checkOut(Receipt receipt) {
	Money total = Money.zero;
	for item : items {
		total += item.getPrice();
		receipt.addItem(item);
	}
	Payment p = acceptCash(total)
	receipt.addPayment(p);
}
```

We have a system that works good if only cash pay method is available, but If we want to include a possibility to pay with credit card we could add that inside if statement like so:
```java
void checkOut(Receipt receipt) {
	Money total = Money.zero;
	for item : items {
		total += item.getPrice();
		receipt.addItem(item);
	}
	Payment p;
	if (credit)
		p = acceptCredit(total);
	else
		p = acceptCash(total);
	receipt.addPayment(p);
}
```
But that violates open-closed principle, because we've modified the algorithms in order to extend it. 
Or we can replace the if statement for an abstraction that handles all payments.

```java
void checkOut(Receipt receipt) {
	Money total = Money.zero;
	for item : items {
		total += item.getPrice();
		receipt.addItem(item);
	}
	Payment p = pm.acceptPayment(total);
	receipt.addPayment(p);
}
```

If we won't modify old modules that they won't ever rot.
It also conforms to how customers think about the software - that adding new feature is adding new feature and not modifying anything.

## Is this possible?
Can you really create such a system that is never required to modify modules that where once implemented?
Theoretically yes - but very hard and impractical. So while you can't make a whole system conform to open-closed principle you can aim to create functions and classes in such a way.


## The Lie
But it is really easy to conform to open-closed principle for a change you expect, it gets harder when you have unexpected change it really does require changing some code. So it really depends on you predicting what may change

## Solution?

### Big Design up Front
Basically try to think of everything - really hard. The problem with this is that it creates a lot of abstractions that can often be unnecessary.

### Agile Design

Ship simple product, and wait for a customer to request changes, and only then protect yourself from change in that area.