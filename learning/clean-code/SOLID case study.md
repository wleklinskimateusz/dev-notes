#SOLID 

## Payroll project
### Design
1. Enumerating all the use cases (or as many as we can think of)
2. Assemble them into use case-driven architecture
3. Choose a couple of the use cases and to a deep dive through their design
4. Implement them (those couple we've chosen) 
5. Repeat 3&4 until we're done

### Requirements
**Use case List**:
- `AddEmployee`
- `DeleteEmployee`
- `ChangeEmployee`
- `AddTimeCard`
- `PayEmployee`
- `AddSalesReceipt`
- `AddServiceCharge`

**Entity List**:
- `Employee
- `TimeCard`
- `CommissiionedEmployee`
- `HourlyEmployee`
- `SalesReceipt`
...

Then we can transform Entity List into Data Dictionary:

### Data Dictionary:
commissioned-employee = base-pay + commission-rate + BI-WEEKLY + pay-disposition
hourly-employee = hourly rate + WEEKLY + pay-disposition
salaried-employee = salary + MONTHLY + pay-disposition

pay-disposition = {mail | PAYMASTER | direct-deposit}
	mail = address
	direct-deposit = account
sales-receipt = date + amount-sold
time-card = date + hours-worked
union-membership  = {MEMBER | NON-MEMBER}

...
transform into:
employee = pay-type + pay-disposition+union-membership
	pay-type = { commissioned | hourly | salaried }
		commissioned = base-pay + commission-rate + BI-WEEKLY
		hourly = hourly-rage + WEEKLY
		salaried = salary + MONTHLY
	pay-disposition = { mail | PAYMASTER | direct-deposit }
		mail = address
		direct-deposit = account
	sales-receipt = date + amount-sold
	time-card = date + hours-worked
	union-membership = { MEMBER | NON-MEMBER }


## Design Session

### Single Responsibility Principle
> Q: Who are the actors in this system?

**Actors**:
- operations (people adding, deleting employees, sales receipts, time cards)
- policy (how much, when people get paid) 
- union (union membership, deduct charges etc)

we need to make as many modules as there are actors

### Open-Closed Principle
We have `AddEmployeeController` (part of the UI) it creates a data structure `AddHourlyEmployeeRequest` and it passed it down to `AddHourlyEmployeeUseCase`

This can be a problem, because each change to the data structure forces the controller to be recompiled, to fix it we must decouple the controller from the data structures and use cases. 

We could create the `RequestBuilder` interface (with methods that build each individual data structure). The implementation of that interface will do the building and it will return those data structure under the degenerate type `Request`

the `UseCaseFactory` interface would have methods in it for creating every possible use case. The implementation of that interface would create those use cases, but would return them as the interface `UseCase`. 

The `UseCase` interface and the `Request` data type would both be use by the controller, to execute the use case.

### The Liskov Substitution Principle

Consider the `AddTimeCard` use case. It is pretty simple. It has to fetch to employee, it has to create a `TimeCard`, and it has to add that `TimeCard` to the`HourlyPay` type object within the `Employee`.

But how does this use case know that the pay type object held by the employee is an hourly pay type? What method does the use case call to add that time card?

```java
public class AddTimeCardUseCase implements UseCase {
	public void execute(Request request) {
		AddTimeCardRequest tcReq = (AddTimeCardRequest) request;
		TimeCard timecard = TimeCard(tcReq.date, tcReq.hours);
		Employee e = employeeGateway.findEmployee(tcReq.employeeId);
		e.getPayType().addTimeCard(timecard);
	}
}
```

but that violates open-closed principle (we would have to add code for each new paytype with specific requirements)

```java
public class AddTimeCardUseCase implements UseCase {
	public void execute(Request request) {
		AddTimeCardRequest tcReq = (AddTimeCardRequest) request;
		TimeCard timecard = TimeCard(tcReq.date, tcReq.hours);
		Employee e = employeeGateway.findEmployee(tcReq.employeeId);
		e.addTimeCard(timecard);
	}
}

puvlic interface PayType {
	public int calculatePay();
	public void addTimeCard(TimeCard tc);
}
```

if we have to specify specific paytype and treat that differently that we're violating Liskov Substitution principle. 

```java
public class AddTimeCardUseCase implements UseCase {
	public void execute(Request request) {
		AddTimeCardRequest tcReq = (AddTimeCardRequest) request;
		TimeCard timecard = TimeCard(tcReq.date, tcReq.hours);
		Employee e = employeeGateway.findEmployee(tcReq.employeeId);
		Hourly hourly = (Hourly) e.getPayType();
		hourly.addTimeCard(timecard);
	}
}
```