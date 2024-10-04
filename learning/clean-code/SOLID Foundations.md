# SOLID Foundations
#SOLID
## The source code is the design

Q: What do engineers produce?
A: Engineers produce documents that specify how to build products

In case of Software engineer this document is a source code
Source code is not a true product, but a set of instruction to create an actual executable program

In software it is cheaper to create a product that it is to design it

## Design Smells

### Rigidity
is the tendency of a system to be hard to change

The system is hard to change when the cost of changing it is high

### Fragility
A system is fragile when small change to one module causes other unrelated modules to misbehave

### Immobility
a system is immobile when its internal components can not be easily extracted and reused in environments. 

### Viscosity
A system is viscous when necessary operations are difficult to perform and take a long time to execute

## Needless complexity

Q: Should we care about possible future feature/extensions or not?
A: we should focus on present designs and requirements, but never be afraid to change the design later (thanks to testing)

## What Is Object Oriented Paradigm?
you can inverse dependencies for a program not to depend on low level details. For that case we create an abstraction that handles that low level details without the knowledge of the entire program

OO is about passing messages. you only care about sending the message and do not care how it will be interpreted and executed

Neither Sender, not Receiver of the don't depend on each other, they only depend on the message which is an abstraction

Essential Quality of OO is the ability to inverse key dependencies protected high-level policies from low-level details







