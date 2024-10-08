# Clean Tests

## Anatomy of the test

### Sort algorithm

We're going to write an algorithm in C.

Let's start with the degenerate tests
>Q: what should we do with passing `null` as input to sort algorithm. Should we return null? or should we return zero-sized array.
>A: If we wanted to return 0-sized array in C we would have to use `malloc` with 0 as an argument.

And that is what we should do!. a zero sized array creates a buffer that must be freed. So the behavior will be consistent with every other input

```c
int* sort(int* unsorted) {
 return (int*)(malloc(0));
}

TEST(sort, null_input)
{
 int* inputArray = NULL;
 int* sortedArray = sort(inputArray);
 CHECK(sortedArray !== NULL);
 free(sortedArray);
}
```

Here apart from the triple As we have 4 A's, so after Arrange, Act, Assert there is Annihilate (free).

## The Arrange and the Annihilate

It's the job of the arrange phase of a test function to drive a system into the state in which it can be tested.

If we have a single test function that it is easy, we arrange, we test and throw it away

Three approaches:

- Transient Fresh (it is created and destroyed around every test)
- Persistent Fresh (survives from test to test but is initialized in the every test)
- Persistent Shared (allows some test to accumulate from test to test)

So in the world where we use `Transient Fresh` approach, we won't need any `teardown` function (`afterEach`) because each time we use entirely new state.

If we need a shared state between multiple tests we would need to have `beforeAll` and `afterAll` those methods would be good to open/close database connections (because it can be expensive to open close before/after each test)

## Test Hierarchy

In some test framework you can nest or group tests and create setup and teardown function for only that group. Those can be nested and ideally you want have to create lots of functions that setup differently depending on what you want. (JS test frameworks do this for example)

```typescript
describe("some test", () => {
 beforeEach(() => {
  console.log("global setup function");
 })

 it("should pass", () => {
  console.log("test");
 })

 describe("nested group", () => {
  beforeEach(() => {
   console.log("function runs before each test in that group");
   console.log("but after global setup");
  })

  it("should also pass", () => {
   console.log("nested test");
  })
 })
})
```

In C# you can inherit TestClasses from each other, so you can nest that way.
Java has many problems with it, it is weird (There is a workaround but never mind)

## Act

usually a single function that is being tested. So this phase is just a call of this function

if you're writing code in functional style that you always need one function call, but if you mutate data inside and you want to test the state change after multiple functions that you must call multiple functions

## The Assert

### Single Assert rule

the `assert` is a boolean operation

amount of physical assertion is irrelevant, as long as they are composed into the single logical assertion.

We don't want to have multiple acts and asserts inside a single test (test should only test one thing)
