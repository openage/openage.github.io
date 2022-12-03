# Definitions

## Roles

### Customer 

- Admin
- Accountant
- Exporter

### Supplier

- Employee

### Yatra

- Sales Agent
- Pricing Agent
- Operator
- Accountant
- Manager

## Task

It is an action item for a user. When a task is created from an order details page (an example of an entity page) is usually associated with that `entity`. When user views the details of the task, the view handler will resolve and send the user to the entity viewer

The system can create (based on the template) and assign it to a user. 
e.g. when an order document is uploaded by customer a `file|review` task is created for the operator of the order

The states of the task is governed by it type. 
e.g. a file|review task may have `pending`, `reviewed`, `rejected` states.

The system can also change the state of the task when the state of the associated entity changes 

## Query

Is a free text task of type `query` assigned to an individual and attached to an order (or any other entity). It results into an action item for the assignee and appears in his to do list

The states of the query are `raised`, `resolved`, `re-opened`

The assignee usually adds clarification/documents and marks the query to resolved
