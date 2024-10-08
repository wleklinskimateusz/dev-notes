# Test Design

Test shouldn't know to much about implementation. So you should test the behavior and not how it is implemented

## SOLID Test

If you applied a small change to the production code and test start to break all over the place than you have fragile tests.

### Single Responsibility in tests

as a general rule one test file should test one class which should align with one responsibility 
(if class has one responsibility too)

### Open/Closed principle

We want the production code to be open for extension, but the tests to be closed for modification

### Dependency Inversion

Test are low level details, so the test should always depend on production code (not the other way around)

## Testing Private function

You shouldn't test private functions, there shouldn't be any pathway to access hidden items.

## Naming tests

When we use triple A's rule we can use that to name our tests:

- Arrange -> **Given**
- Act -> **When**
- Assert -> **Then**

we can use given in setup when grouped tests
