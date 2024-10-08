# Advanced Test Driven Development

## A unit in unit tests?

>unit test: Very small test written by programmers for programmers

## Mocks

- Dummy - test double that return degenerate values (null)
- Stub - hard-coding returning value (for example always returning `true`)
- Spies - the same as stub but remembers what happened (number of calls for example)
- Mock - a spy

- Fake is a simulator (has business rules in it). For example authenticator only returns based on fake data) -
`if token == "valid" then return true`
