# Test Process

## Simple Techniques

### Fake it till you make it

We make a test case pass by faking it (implicitly return what is expected), then we make another test case pass
by faking it a little more, and we keep adjusting the code until it is generic.

It works if we focus on gradually make more complex test cases, but start with very simple ones.

### Stairstep test

Sometimes the whole purpose of a test is so you can write next test, and when you have written the second test,
then the first test has no purpose and you can delete it.

### Assert first

A technique that we start by creating assertion and then set everything up so that the assertion makes sense
(we have to crreate all the variables, function calls) - we have to deal with compile and execution errors.

### Trangulation

We create a test and a dumb implementation that just returns what we expect, and then add another test
that is very similar to the first one but expects different value.
So we have to generlize to solution to make this test pass.

### One to many

The best way to a list or array of object is to deal with one object first.

_____

>Test the behavior and not the API

## Test design

when it comes to production code, we could follow three rules:

1. First make it work
2. Then make it right
3. Then make it fast and small

But when it comes to writing tests, we should add additional rule at the beginning:

1. Make tests expressive (so that the intent of the author is well represented)
2. First make it work
3. Then make it right
4. Then make it fast and small
