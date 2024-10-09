# Transformation Priority Premise

## Refactor vs Transformation

> **Refactor** is a change of code that results in change in structure and no significant change in behavior

> **Transformation** is a change of behavior with no significant change in behavior

## Transformation List:
1. Null
2. Null to constant
3. Constant to variable
4. Add computation
5. Split flow (if statement) into two
6. Variable to array
7. Array to container (generate an array into something like a set, queue etc)
8. If to while
9. Recurse
10. Iteration (usually a for loop)
11. Assign (alter the state of previously initialized variables)
12. Add case (else if to existing if)

We should try to use transformations according to this list priority.