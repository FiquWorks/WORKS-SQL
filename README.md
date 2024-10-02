```SQL
Microsoft Windows [Version 10.0.19045.4894]
(c) Microsoft Corporation. All rights reserved.

C:\Users\User>sqlplus

SQL*Plus: Release 21.0.0.0.0 - Production on Tue Oct 1 15:35:07 2024
Version 21.3.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.

Enter user-name: mplsql
Enter password:
Last Successful login time: Tue Oct 01 2024 15:23:26 +03:00

Connected to:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

SQL> grant all privileges to mplsql;

Grant succeeded.

SQL> CREATE TABLE Students (    StudentID INT PRIMARY KEY,    FirstName VARCHAR(100),    LastName VARCHAR(100),    Email VARCHAR(100),    DateOfBirth DATE);

Table created.

SQL> exit
Disconnected from Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

C:\Users\User>sqlplus

SQL*Plus: Release 21.0.0.0.0 - Production on Tue Oct 1 15:54:19 2024
Version 21.3.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.

Enter user-name: mplsql
Enter password:
Last Successful login time: Tue Oct 01 2024 15:41:49 +03:00

Connected to:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0


SQL> CREATE TABLE Professors (    ProfessorID INT PRIMARY KEY,    ProfessorName VARCHAR(100),    Department VARCHAR(100),    Email VARCHAR(100));

Table created.

SQL> CREATE TABLE Courses (    CourseID INT PRIMARY KEY,    CourseName VARCHAR(100),    CreditHours INT,    ProfessorID INT,    FOREIGN KEY (ProfessorID) REFERENCES Professors(ProfessorID) ON DELETE SET NULL);

Table created.

SQL> CREATE TABLE Attendance (    AttendanceID INT PRIMARY KEY,    StudentID INT,    CourseID INT,    AttendanceDate DATE,    Status VARCHAR(10),    FOREIGN KEY (StudentID) REFERENCES Students(StudentID) ON DELETE CASCADE,    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID) ON DELETE CASCADE);

Table created.

SQL> INSERT INTO Students (StudentID, FirstName, LastName, Email, DateOfBirth) VALUES (1, 'Michael', 'Johnson', 'michael.johnson@student.com', TO_DATE('2001-06-15', 'YYYY-MM-DD'));

1 row created.

SQL> INSERT INTO Students (StudentID, FirstName, LastName, Email, DateOfBirth) VALUES (2, 'Sara', 'Connor', 'sara.connor@student.com', TO_DATE('1999-12-05', 'YYYY-MM-DD'));

1 row created.

SQL> INSERT INTO Professors (ProfessorID, ProfessorName, Department, Email) VALUES (1, 'Dr. John Smith', 'Computer Science', 'john.smith@university.edu');

1 row created.

SQL> INSERT INTO Professors (ProfessorID, ProfessorName, Department, Email) VALUES (2, 'Dr. Jane Doe', 'Mathematics', 'jane.doe@university.edu');

1 row created.

SQL> INSERT INTO Professors (ProfessorID, ProfessorName, Department, Email) VALUES (3, 'Dr. Albert Davis', 'Physics', 'albert.davis@university.edu');

1 row created.

SQL> INSERT INTO Courses (CourseID, CourseName, CreditHours, ProfessorID) VALUES (1, 'Physics 101', 4, 3);

1 row created.

SQL> INSERT INTO Courses (CourseID, CourseName, CreditHours, ProfessorID) VALUES (2, 'Math 101', 3, 2);

1 row created.

SQL> INSERT INTO Courses (CourseID, CourseName, CreditHours, ProfessorID) VALUES (3, 'Computer Science 101', 5, 1);

1 row created.

SQL> INSERT INTO Attendance (AttendanceID, StudentID, CourseID, AttendanceDate, Status) VALUES (1, 1, 1, TO_DATE('2024-10-01', 'YYYY-MM-DD'), 'Present');

1 row created.

SQL> INSERT INTO Attendance (AttendanceID, StudentID, CourseID, AttendanceDate, Status) VALUES (2, 2, 2, TO_DATE('2024-10-01', 'YYYY-MM-DD'), 'Absent');

1 row created.

SQL> commit;

Commit complete.

SQL> exit
Disconnected from Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

C:\Users\User>INSERT INTO Attendance (AttendanceID, StudentID, CourseID, AttendanceDate, Status) VALUES (2, 2, 2, TO_DATE('2024-10-01', 'YYYY-MM-DD'), 'Absent');

SQL> ALTER TABLE professors
  2  ADD studentid INT;

Table altered.


SQL> ALTER TABLE professors
  2  ADD CONSTRAINT fk_studentid
  3  FOREIGN KEY (studentid) REFERENCES students(studentid);

Table altered.

SQL> INSERT INTO Students (StudentID, FirstName, LastName, Email, DateOfBirth)VALUES (3, 'David', 'Miller', 'david.miller@student.com', TO_DATE('1999-12-05', 'YYYY-MM-DD'));

1 row created.

SQL> INSERT INTO Courses (CourseID, CourseName, CreditHours, ProfessorID)VALUES (4, 'History 101', 3, 1);

1 row created.

SQL> INSERT INTO Attendance (AttendanceID, StudentID, CourseID, AttendanceDate, Status)VALUES (3, 3, 1, TO_DATE('2024-10-01', 'YYYY-MM-DD'), 'Present');

1 row created.

SQL> UPDATE Students SET Email = 'michael.johnson2024@student.com'WHERE StudentID = 1;

1 row updated.

SQL> UPDATE Courses SET CreditHours = 5WHERE CourseID = 4;

1 row updated.

SQL> DELETE FROM Attendance WHERE AttendanceID = 2;

1 row deleted.

SQL> SELECT s.FirstName, s.LastName, a.Status, a.AttendanceDate
  2  FROM Students s
  3  JOIN Attendance a ON s.StudentID = a.StudentID;

FIRSTNAME
--------------------------------------------------------------------------------
LASTNAME
--------------------------------------------------------------------------------
STATUS     ATTENDANC
---------- ---------
Michael
Johnson
Present    01-OCT-24

David
Miller
Present    01-OCT-24

FIRSTNAME
--------------------------------------------------------------------------------
LASTNAME
--------------------------------------------------------------------------------
STATUS     ATTENDANC
---------- ---------

SQL> ALTER TABLE Professors ADD PhoneNumber VARCHAR(15);

Table altered.

SQL> UPDATE Courses SET CreditHours = 4 WHERE CourseID = 1;

1 row updated.

SQL> commit;

Commit complete.

SQL> ROLLBACK;

Rollback complete.


  



```
