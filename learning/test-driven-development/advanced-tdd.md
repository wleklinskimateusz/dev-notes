# Advanced Test Driven Development Part 1

## The Laws of TDD
1. You're not allowed to write any production code until you've got a unit test failing
2. Don't write more tests then it is sufficient to fail even if that failure is just the failure to compile (move to writing production code that will make this test pass)
3. Stop writing production code as soon as test passes and then go back to writing tests

Remember to refactor frequently

> it's best to start writing tests from the degenerate tests (like check for `undefined` or empty string)

## Triple A-rule
1. Arrange
2. Act
3. Assert

Every unit test should be broken up into those three parts
**Arrange** is setting up the test
**Act** is calling a function to be tested
**Assertion** is testing if the result are what we aspect. This is a logical assertion, not necessarily an assertion call (so we can have multiple assertion calls in one logical assertion) 

## Incremental Algorithmics
>As the tests get more specific the code gets more generic

The idea that you can write any algorithm by incrementally adding solutions to next test cases

## Getting Stuck
you're stuck if there's nothing incremental you can do to pass the currently failing test

>Q: Why is it happening?
>A: Either you wrote the wrong test, or making the production code too specific (or both)

Soo, how no to get stuck?
best idea is to write test in such a way that they force you to introduce complexity gradually. (So start from simple, degenerate examples, and step by step move to something more challenging)
