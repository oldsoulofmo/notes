```sql
CREATE PROCEDURE GetCourseStudentCount (@CourseID CHAR(10))
AS
BEGIN
    SELECT c.Cname, COUNT(sc.Sno) AS StudentCount
    FROM Course c
    JOIN SC sc ON c.Cno = sc.Cno
    WHERE c.Cno = @CourseID
    GROUP BY c.Cname;
END;
GO
EXEC GetCourseStudentCount 'c01';
```

This is a procedure where the parameter CourseID is a string of 10 chars. 

```sql
CREATE TRIGGER UPDATEblabla
ON SC
AFTER INSERT
AS
BEGIN
	UPDATE cyolumn
	SET Strength = Strength +1
	WHERE cno IN (SELECT cno FROM Inserted);
END;
GO
```

This is a trigger for when there is insertion on the SC table, we update the cyolumn then. 

```sql
CREATE TRIGGER Deleteblabla
ON student
AFTER DELETE
AS
BEGIN
	DELETE FROM sc
	WHERE sno IN (SELECT sno FROM deleted);
END;
```

A trigger for when a record from student table is deleted we delete from sc too then. 



