//creating the employee and depatment table
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50) NOT NULL,
    Location VARCHAR(100)
);

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50) NOT NULL,
    DeptID INT,
    Salary DECIMAL(10, 2),
    HireDate DATE,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
//inserting values
INSERT INTO Department (DeptID, DeptName, Location) VALUES (1, 'IT', 'New York');
INSERT INTO Department (DeptID, DeptName, Location) VALUES (2, 'HR', 'London');

INSERT INTO Employee (EmpID, EmpName, DeptID, Salary, HireDate) 
VALUES (1, 'John Doe', 1, 50000.00, '2020-01-15');
INSERT INTO Employee (EmpID, EmpName, DeptID, Salary, HireDate) 
VALUES (2, 'Jane Smith', 1, 60000.00, '2019-05-20');
//integrity constraints
ALTER TABLE Employee
ADD CONSTRAINT chk_salary CHECK (Salary >= 0);
ALTER TABLE Employee
ADD CONSTRAINT chk_hire_date CHECK (HireDate <= CURDATE());
//bilt-in functions
SELECT COUNT(*) AS TotalEmployees FROM Employee;
SELECT AVG(Salary) AS AvgSalary FROM Employee;
//joins and sorting
SELECT EmpName, DeptName 
FROM Employee 
INNER JOIN Department ON Employee.DeptID = Department.DeptID;
UPDATE Employee
SET Salary = Salary * 1.1 -- Increase salary by 10%
WHERE EmpID = 1;
DELETE FROM Employee
WHERE EmpID = 2;
SELECT EmpName, Salary
FROM Employee
WHERE Salary = (SELECT MAX(Salary) FROM Employee);
SELECT DeptName, COUNT(*) AS NumEmployees
FROM Employee
INNER JOIN Department ON Employee.DeptID = Department.DeptID
GROUP BY DeptName;
SELECT EmpName, HireDate
FROM Employee
WHERE HireDate > '2023-01-01';
