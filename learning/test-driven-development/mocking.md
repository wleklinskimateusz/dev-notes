# Mocking
#testing

## Test Doubles
using fake classes to test some behavior without involving the whole system.

### The Dummy
A fake class that implements required methods and returning degenerate values (as close to null or zero as possible)

### The Stub
A Dummy that returns some hard-coded value. It can drive the test to specific pathways in which different cases for the production code can be tested

### The Spy
a Stub that can track how many times is function called and with which arguments

### The Mock
a spy that knows what should happen, so the logic of this has an implementation that depend on what it is tested. (For example it saves the data from the calls in order to verify the assertion)



## Two Schools of TDD:
### The Mockists 
>(the London School)

Focus on using spies to verify the implementation of algorithms. They tolerate the coupling of production code to the tests for the cost of better assurance the the algorithm works for each input 


### The Statists
> (The Chicago School, the Detroit School or the Cleveland School)

It puts more emphasis to the values returned by a function and prefers to decouple the tests from the algorithms they test

### What should I use?
>Q: Which is better?
>A: Both, and neither

the Spies are very useful when crossing the boundary of the system (mocking the UI, Database handlers and so on).

When you're not testing something that is on the boundary then, it is probably better to test the values.

## Mocking Patterns
### Test Specific Subclass
When you want to test a function in the class but you want to modify the behavior of other functions in that class you can create a class inside a test that inherits from the class you want to test and mock/spy on some methods in order for them to change some value in the scope of the test.

### Self-Shunt
similar to the above, but you can make the test class implement the interface that you need mocked. And later in the class we want to test pass Testing Class as an implementation of an interface.

### Humble Object
Reducing the object near the boundary that is basically nothing to test
and test only the connection to those objects.





