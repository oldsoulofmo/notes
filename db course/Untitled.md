```sql
1. Establish the login account of user 1 and user2 as SQL Server authentication. 

  

CREATE LOGIN user1 WITH PASSWORD = '1A2a3b4b5c6c';

CREATE LOGIN user2 WITH PASSWORD = '1a2A3b4b5c6c';

  

  

1. Mapping the user1 and user2 as the legal user of database“student”.

  

USE student;

  

CREATE USER user1 FOR LOGIN user1;

CREATE USER user2 FOR LOGIN user2;

  

  

  

1. Grant user1 the select authority for student table, grant user2 the insert authority for student table. 

  

GRANT SELECT ON student TO user1;

  

GRANT INSERT ON student TO user2;

  

  

  

1. Login as user1 and user2. Execute select * from student and insert into student values(‘9512104’,’Zhang San’,’male’,20,’CS’). If this can successfully implemented?

  

SELECT * FROM student; -- This should succeed because user1 has SELECT permission.

INSERT INTO student VALUES ('9512104', 'Zhang San', 'male', 20, 'CS'); -- This should fail because user1 does not have INSERT permission.

  

  

  

  

1. Create a new ROLE1 in database of student, add user1 and user2 as role member.  
    

CREATE ROLE ROLE1;

  

-- Add user1 and user2 to the role

ALTER ROLE ROLE1 ADD MEMBER user1;

ALTER ROLE ROLE1 ADD MEMBER user2;

  

  

  

1. Grant the ROLE1 the insert, delete and query authority on student table.

  

GRANT SELECT, INSERT, DELETE ON student TO ROLE1;

  

  

  

1. Login as user2 and user3. Execute select * from student and insert into student values(‘9512104’,’Zhang San’,’male’,20,’CS’). If this can successfully implemented?

  

First we create user3 : 

  

CREATE LOGIN user3 WITH PASSWORD = 'password3';

CREATE USER user3 FOR LOGIN user3;

  

SELECT * FROM student; -- This should fail because user3 does not have SELECT permission.

INSERT INTO student VALUES ('9512105', 'Li Si', 'male', 21, 'Math');   -- This should fail because user3 does not have INSERT permission.
```