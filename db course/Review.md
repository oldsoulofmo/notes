Integrity constraints guard against accidental damage to the database.
- Entity integrity. (primary key)
- Referential integrity. (foreign key)
- User-defined integrity. 

> Relational algebra works on relations, by combinations and division of relations the user can obtain personalized data set.


- Union.
- Intersection.
- Difference.
- Cartesian product. 

Relational calculation  : 
- select.
- project.
- join.

$\sigma_{\mathrm{F}}(R)=\left\{t \mid t \in R \wedge F(t)=\text { 'TRUE' }\right\}$
- Select from R the tuples that meet the condition F.

$\Pi_A(R)=\{t[A] \mid t \in R\}$ 
- Select some columns A of tuples from R.

Join is to select the tuples that meet the conditions from the cartesian product of two relations. 

-  Outer schema : the user schema, it's a local description of data users are interested in. a database has several outer schemas.
 - Logical schema : conceptual schema or just schema, it's the description of logical structure and feature of all data. ( a common view for all users)
- Inner schema : physical schema, it's the overall physical structure of the database. 
- View : an object in db, which is a mechanism that is provided by the dbms for users to access the data from several perspectives.
- View is a virtual relation, does not save data, data is saved in the basic relation.
- View can extract data from more than one relation.
- Transaction : a unit of program execution that accesses and possibly updates various data items.

##### ACID Properties 

To  preserve the integrity of data the DBS must ensure acid props : 

- Atomicity : Either all ops of the transactions are properly reflected in the db or none are.
- Consistency : Execution of a transaction in isolation preserves the consistency of the db.
- Isolation : Multiple transactions may execute concurrently but each transaction must be unaware of other concurrently executing transactions. Intermediate transaction results must be hidden from other concurrently executed transactions. 
- Durability : After a transaction completes successfully, the changes it has to the db persist even if there are system failures.

##### Concurrent executions 

Multiple transactions are allowed to run concurrently in the system.
###### Advantages 

- Increased processor and disk utilization, leading to better transaction throughput.
- Reduced average response time for transactions : short transactions do not need to wait behind long ones.

##### Concurrency control 

In the DBS, the chief method for concurrency control is locking.

Locking constrain the operations on data item in and outside the transaction.

##### Lock based protocols 

A lock is a mechanism to control concurrent acces to a data item.

Data item can be locked in two modes : 
- Exclusive (x) mode : data item can be both read and written.
- Shared (s) mode : data item can only be read.

> Transaction can proceed only after request is granted.


##### Lock compatibility matrix 

|     | S     | X     |
| --- | ----- | ----- |
| S   | true  | false |
| X   | false | false |

##### Security control 

It provides the db security in different levels, preventing intentional or unintentional destroy on data.

- Validate if a login account is a valid user of sql server.
- Validate if a user is a valid user of a db.
- Validate if a user has the authority for some operations.

The relations in the DB should satisfy some normalization principles. 
1NF , 2NF , 3NF , BCNF , 4NF , 5NF.


- A trigger is a statement that is executed automatically by the system as a side effect of a modification to the db.

- Grant.
- Revoke.
- Deny.

```sql
  

CREATE LOGIN user1 WITH PASSWORD = '1A2a3b4b5c6c';

CREATE LOGIN user2 WITH PASSWORD = '1a2A3b4b5c6c';
```