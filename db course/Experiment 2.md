To fin the birth year of students : 

```sql
SELECT Sname,2024-Sage AS birthYear FROM student
```

To find the total number of students : 

```sql
SELECT COUNT(*) AS Total FROM student
```

To join two tables we join them (inner-join) from their common point : 

```sql
SELECT student.sno, student.sname, sc.cno, sc.mark FROM student
INNER JOIN sc ON student.sno = sc.sno
```

To add a condition on the join we must leave it at the end of statements : 

```sql
SELECT student.sname, sc.cno, sc.mark FROM student
INNER JOIN sc ON student.sno = sc.sno
WHERE Sdept = 'CS'
```

> Here what we choose to display on query is definitely our choice. 

```sql
SELECT student.sname, c_volumn.cname, sc.mark FROM student
INNER JOIN sc ON student.sno = sc.sno
INNER JOIN c_volumn ON sc.cno = c_volumn.cno
WHERE cname = 'VB' AND Sdept = 'IS'
```

```sql
SELECT student.sname,student.Sdept FROM student
INNER JOIN sc ON student.sno = sc.sno
INNER JOIN c_volumn ON sc.cno = c_volumn.cno
WHERE cname = 'VB'
```

Using a subquery to query a very specific data that match the data of `Zhang's departement` :

```sql
SELECT student.sname AS name,student.Sdept AS departement FROM student
WHERE Sdept = (SELECT Sdept FROM student WHERE Sname = 'Zhang Hai')
```

To find students who are enrolled in the course of "database" : 

```sql
SELECT student.sname,sno FROM student
WHERE sno IN (SELECT sno FROM sc
JOIN Course ON Course.cno = sc.cno
WHERE Cname = 'Database')
```

To find students who are enrolled on `c02` and have a mark superior to the average of `c02`: 

```sql
SELECT sno, mark FROM sc
WHERE cno = 'c02' AND mark > (SELECT AVG(mark) FROM sc WHERE cno = 'c02' )
```

To find students who are enrolled on `c01`, display the student’s name : 

```sql
SELECT sname FROM student
WHERE sno IN (SELECT sno FROM sc WHERE cno ='c01')
```

> The thing about subqueries here is that we can use the parallelism of an attribute being present in two different tables like the student ID and then query based on conditions. 


```sql 
SELECT sname,Sdept FROM student
WHERE sno NOT IN (SELECT sno FROM sc WHERE cno ='c01')
```

Use subquery to get the sum course credits the student ‘Li Yong ’takes : 

```sql
SELECT SUM(Ccredit) AS total_credits FROM Course
WHERE cno IN (SELECT cno FROM sc WHERE sno = '9512101')
```

Oldest fella : 

```sql
SELECT Sname,Sage FROM student
WHERE Sage = (SELECT MAX(Sage) FROM student)
```

Null marks :
```sql 
SELECT Sname, Sdept FROM student
WHERE Sno IN (SELECT sno FROM sc WHERE mark IS NULL)
```

Average score for maths department :

```sql
SELECT AVG(mark) FROM sc
WHERE sno IN (SELECT sno FROM student WHERE Sdept = 'MA')
```

```sql
-- Insert into Student table
INSERT INTO Student (Sno, Sname, Ssex, Sage, Sdept)


-- Insert into SC table
INSERT INTO sc (sno, cno, mark, c_type)
VALUES ('9512110', 'c01', 80, 'compulsory');
```

```sql
UPDATE student
SET sage = sage +1;
```

```sql
UPDATE sc
SET mark = 0 WHERE sno = '95121..';
```

```sql
UPDATE sc
SET mark = mark + 10 
WHERE sno = '9512103' AND cno = 'c04';
```

```sql
DELETE FROM sc 
WHERE cno = 'c04';
```

```sql
DELETE FROM sc
WHERE sno = '9512102';
```

