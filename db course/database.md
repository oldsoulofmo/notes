DB is the long term stored, structured, shared large amount of data in the computer. 

DBMS (database management system)
- A software between user and operating system.
- Organize, store, obtain and maintain the data effectively. 

It contains information about a particular enterprise :
- Collection of interrelated data.
- Set of programs to access the data.
- An env. that is both convenient and efficient to use.

DBS (database system) : The system that installs the db in the computer.

## Database system architecture 

Data model is a collection of tools for describing : 
- data.
- data relationships.
- data semantics.
- data constraints.

> Modeling the real world scenarios. 

#### Data model 

conceptual model -> logical model -> physical model 

conceptual model : 
- it is a tool for db design.
- a comm language for user and db designer.
- a bridge between reality and computer. 

We have the ER model : Entity Relationship model. 

- The ER model was developed to facilitate db design. 
- The ER model is very useful in mapping the meaning and interactions of real world enterprises onto a conceptual schema. 

#### ER model 

Entity : an object that exists and is distinguishable from other objects. 
Attribute : descriptive properties possessed by all members of an entity set. 
Relationship : relationship between entities. 

#### Entity 

example : specific person, company, event, plant.
Ticket system : flight , traveler , airport.

> An entity set is a set of entities of the same type that share the same props. 
> Example : set of all persons, companies, tress, holidays. 


in the ER diagram, the entity is represented as a rectangle.

#### Attributes 

They are descriptive props possessed by all members of an entity set. 

`course=(course_id,title,credits)` 

> relationship is represented by a diamond. 


#### cardinality constraints 

- One to one (1:1).
- One to many (1:n).
- Many to one (n:1).
- Many to many (m:n).

(check paper hand for details).

#### Degree of a relationship 

##### Binary relationship 

- involves two entity sets.
- most relationship sets in a dbs are binary. 

 ex of a relationship between more than two entities : (customer, seller and product).

#### steps to design E-R diagram 

- determine the entity.
- determine the relationship and it's type.
- determine the attributes of entity and relationship.
- modify the ER diagram.

### Logical model 

One thing to note here is that logical model is a relational model. 

> In the relational model a table is used to organize data, it's called a relation. 
> The relation db is a set of relations. 

| ID     | name | dept_name |
| ------ | ---- | --------- |
| 22222  | eins | physics   |
| 123131 | wp   | finance   |
| 311333 | qw   | history   |
so here the columns are attributes and rows are tuples. 


> [!NOTE] Note
> Order of tuples is irrelevant.

- the set of allowed values for each attribute is called the domain of the attribute.
- attribute values are normally required to be atomic, that is indivisible. 
- the special null value is a member of every domain, indicating that the value is unknown.

instructor = (ID,name,dept_name,salary) is a relation schema. 


> [!NOTE] Note
> R = (A1,A2,...,An) is a relation schema and A's are attributes. 



![[Untitled.jpg]]

_Answer :_ 

- (22222,Einstein,Physics,95000) is a tuple. 
- The **primary key** uniquely identifies each row in the relation. In this table, the **ID** column is the primary key since each value in this column is unique.
- Attributes are ID name dept_name salary.
- Schema : Employee = (ID : integer , name : string ,dept_name : string ,salary : integer).

#### Data manipulation in the relational model 

Data manipulation include <mark style="background: #FFF3A3A6;">query, insert, delete and modify data.</mark>

#### Integrity constraints 

They guard against accidental damage to the db by ensuring that authorized changes to the db do not result in a loss of data consistency. 

There are three types of integrity constraints : 
- entity integrity.
- referential integrity.
- user-defined integrity. 

##### Entity integrity 

A relation must have a primary key in the relational db.

> There is no record without primary key, and it cannot be NULL.

##### Referential integrity 

Ensure the value of attributes appears in a relation also appears in the value of attributes in another relation. 

> Foreign key is used to do the referential integrity. 

##### User defined integrity 

Also called the domain integrity, it specifies the range of attributes. 

For example : 
- A checking account must have a balance greater than 10,000.00$.

#### From ER to relational model 

First thing just transfer the attributes of the ER into the relation (very obvious).

If 1:1 then add the primary key of one of the entities into the relation schema of another entity. 

If 1:n then add the primary key of the 1 entity to the relation of the n entity. 

If n:m relationship between two entities then three relations can be obtained, How ? 
- The relationship itself is transferred into a relation.
- The primary keys of the two entities and the attributes of the relationship are transferred into the attributes. 

- [x] see the screenshots of the last example. 


## Relational algebra 

> Unions, intersection and cartesian products. 
> 
#### Relational calculation 

##### Select 

$\sigma_{\mathrm{F}}(R)=\left\{t \mid t \in R \wedge F(t)=\text { 'TRUE' }^{\prime}\right\}$

- Select from T the tuples that meet the condition F.

##### Project 

$\Pi_A(R)=\{t[A] \mid t \in R\}$ 

- Select some columns A of tuples from R.


> [!NOTE] Composition of operations 
> build expressions using multiple operations. 

##### Join 

- Choose from the tuples that meet the conditions from the cartesian product of two relations.

##### Equi-join 

- (-) is =. 
- select tuples from the cartesian product of r and s where the attributes A and B are equal. 

##### Natural join 
- A special equijoin.
- The compared attributes are the same.
- remove the repeated columns in the results. 



### Introduction to sql 

> Structured query language, at IBM as part of system R project at the IBM san jose research lab.

#### Domain types 

`char` uses a fixed length and pads the string with spaces if the length used is less than the declared. 

`varchar` is a variable length and uses as much storage as needed for the actual string. 

`numeric(p,d)` fixed point number with user specified precision of p digits with d digits to the right of decimal point.

```sql
create table instructor (ID char(5), name varchar(20), dept_name varchar(20), salary numeric(8,2));
```

```sql
CREATE TABLE Course_take (
	Course_id char(8),
	Teacher_id char(10),
	Take_year char(4) NOT NULL,
	Take_semester SMALLINT NOT NULL,
	Teacher_role char(20) CHECK (Teacher_role IN ('speaker','assistant','experiment_instructor')),
	PRIMARY KEY (Course_id,Teacher_id),
	FOREIGN KEY (Course_id) REFERENCES Course(Course_id),
	FOREIGN KEY (Teacher_id) REFERENCES Teacher(Teacher_id)
);
```

```sql
CREATE TABLE Course (
    Course_id CHAR(8) PRIMARY KEY,
    Course_name VARCHAR(30) NOT NULL,
    credit SMALLINT CHECK (credit BETWEEN 1 AND 8),
    semester SMALLINT CHECK (semester BETWEEN 1 AND 12),
    Course_type VARCHAR(10) CHECK (Course_type IN ('compulsory', 'optional')),
    Exam_type CHAR(8) CHECK (Exam_type IN ('exam', 'report')),
    Class_hour SMALLINT CHECK (Class_hour < 68),
    Practice_hour SMALLINT
);
```

To insert into the course table : 

```sql
INSERT INTO Course (Course_id, Course_name, credit, semester, Course_type, Exam_type, Class_hour, Practice_hour)  VALUES 
('C0000004', 'Operating Systems', 4, 5, 'compulsory', 'exam', 55, 18);

```

To delete all the tuples : 

```sql
delete from student
```

To drop :

```sql
drop table r;
```

#### Data manipulation 

##### Data query 

> sql names are case insensitive.

Select info of all students :

```sql
SELECT * From Student
```

- * : all attributes.

The `SELECT` clause can contain arithmetic expressions like $+-*/$, and also constants or functions. 


To find for example the students name and birth year : 

```sql
SELECT Sname, 2023-Sage FROM Student
```

Here for example we calculate the age by implicitly including `2023-Sage`. 

##### Rename column 

> We can rename relations and attributes using the `as` clause.
> `oldName as newName`.

```sql
SELECT Sname,2023-Sage as birth_year FROM Student
-- also correct
SELECT Sname,2023-Sage birth_year FROM Student
```

- SQL allows duplicates in relations as well as in query results.

> To force elimination of duplicates, user `DISTINCT` after `SELECT`.

```sql
SELECT DISTINCT Sno FROM SC
```

> The keyword `all` specifies that duplicates should not be removed. 

```sql
SELECT ALL dept_name FROM Instructor
```

##### Where 

It specifies conditions that the results must satisfy. 

```sql
SELECT ... FROM ... 
WHERE conditions 
```

| Conditions | Predicate                      |
| ---------- | ------------------------------ |
| compare    | =,>,>=,<>(!=)                  |
| range      | BETWEEN AND<br>NOT BETWEEN AND |
| set        | IN, NOT IN                     |
| string     | LIKE, NOT LIKE                 |
| null       | IS NULL, IS NOT NULL           |
| combined   | AND, OR                        |

> [!QUESTION] Predicates
> Find students name, department, age (range is 20 ~ 23).


```sql
SELECT Sname,Sdept,Sage FROM Student 
WHERE Sage BETWEEN 20 AND 23
```


> [!QUESTION] As above
> Find the students name and gender from the department of information, mathematics and computer science.

```sql
SELECT Sname, Sgen FROM Student
WHERE Sdept IN ('Info','Math','CS')
--
SELECT Sname, Sgen FROM Student 
WHERE Sdept = 'info' OR Sdept = 'Math' OR Sdept = 'CS'
```

##### String operations 

 The op `like` use patterns that are described using two special characters : 
- `%` matches any substring.
- `_` matches any character.

```sql
SELECT name FROM Instructor 
WHERE name LIKE '%dar$'
```

Here we find the names of all instructors that have the substring dar in their names.

> Patterns are case sensitive.


> [!EXAMPLE] Pattern matching examples
> - `'Intro%'` matches any string beginning with "Intro".
> - `'%Comp%'` matches any string containing "Comp" as a substring.
> - `'---'` matches any string of exactly 3 chars.
> - `'---%'` matches any string of at least 3 chars.

```sql
SELECT Sname,Sno FROM Student 
WHERE Sname LIKE '_[eu]%'
```

Here we find students with the second char of their name is either e or u. 

> 5 + null returns null.


```sql 
SELECT Sno,Cno FROM Sc 
WHERE Grade IS NOT NULL
```

To find all male students with age below 20 : 

```sql
SELECT * FROM Student 
WHERE age<20 AND Sgen='male'
```

##### Order

```sql
SELECT DISTINCT name FROM Instructor order by name 
```


- order by name desc/asc.
- order by dept_name,name (sort by multiple attributes).

##### Aggregate functions 

- avg 
- min
- max
- sum
- count : n. of values

```sql
SELECT AVG(salary) FROM Instructor WHERE dept_name='CS'
```

> Calculation can not appear in the where clause.

```sql
SELECT Cno,COUNT(No) as number FROM Table 
GROUPE BY Cno
```

> Attributes in select clause must appear in group by list.

```sql
SELECT Sno FROM Sc 
GROUP BY Sno 
HAVING COUNT(*) > 3
```

##### Cartesian product 

```sql
SELECT * FROM Instructor,teaches
```

It generates every possible instructors - teaches pair, with all attributes from both relations.

#### View 

> View is an object in db, it is a mechanism that is provided by the DBMS for users to access the data from several perspectives.

- Provides a mechanism to hide certain data from the view of certain users.
- Any relation that is not of the conceptual model but is made visible to a user as a virtual relation is called a view.
- The virtual relation only saves the definition but not the data.
- When the data in the basic relation changes then the data found from the view also changes.
- View is like a window where a user can access the data he's interested in.
- View is a virtual relation that does not save data. Data is saved in the basic relation. 
- View can extract data from more than one relation.

```sql
CREATE VIEW IS_STUDENT 
AS
SELECT Sno,Snam.Sage
FROM Student
WHERE Sdept='IS';

SELECT * FROM IS_STUDENTS;
```


### Transaction 

> It is a unit of program execution that accesses and can updates various data items. 

For example a transaction to 50$ from account A to account B.

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

- Validate if a login account is a vlid user of sql server.
- Validate if a user is a valid user of a db.
- Validate if a user has the authority for some operations.

The relations in the DB should satisfy some normalization principles. 
1NF , 2NF , 3NF , BCNF , 4NF , 5NF.

### Procedure 

It is compiled when creating, so it runs faster than sql sentences. 

> The procedure provides good performance, security, accuracy and reduce network congestion.

```sql
CREATE PROCEDURE sc_cno_number 
AS 
SELECT Cnp,COUNT(sno) cvolumn 
FROM SC
GROUP BY Cno
```

Procedures can have parameters. 

#### Triggers 

- DML trigger : insert/delete/update.
- DDL trigger : create/alter/drop.

> A trigger is a statement that is executed automatically by the system as a side effect of a modification to the db.


> [!NOTE] Reminder
> Learn triggers from an experiment.

#### Manage authority 

- Grant.
- Revoke.
- Deny.


> [!NOTE] Reminder
> Learn to manage authority from an experiment.



---
Things to learn from the experiment 2  :

- JOIN.
- SUBQUERIES.
- ANY, SOME, ALL.
- DATA UPDATE.

Thing to learn from experiment 3 : 

- View. 



