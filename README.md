domashka15
domashka15 - робив по незнанці , з GPT 
-- - - -- - -- -- - - -
CREATE DATABASE IF NOT EXISTS CompanyDB;
USE CompanyDB;
CREATE TABLE Projects (
    ProjectID INT PRIMARY KEY,
    ProjectName VARCHAR(255) NOT NULL
);
CREATE TABLE Tasks (
    TaskID INT PRIMARY KEY,
    TaskName VARCHAR(255) NOT NULL,
    ProjectID INT,
    DueDate DATE,
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(255) NOT NULL,
    ProjectID INT,
    TaskID INT,
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID),
    FOREIGN KEY (TaskID) REFERENCES Tasks(TaskID)
);
INSERT INTO Projects (ProjectID, ProjectName) VALUES
(1, 'Проєкт 1'),
(2, 'Проєкт 2');

INSERT INTO Tasks (TaskID, TaskName, ProjectID, DueDate) VALUES
(1, 'Завдання 1', 1, '2024-01-15'),
(2, 'Завдання 2', 1, '2024-02-01'),
(3, 'Завдання 3', 1, '2024-02-15'),
(4, 'Завдання 1', 2, '2024-01-20'),
(5, 'Завдання 2', 2, '2024-02-10'),
(6, 'Завдання 3', 2, '2024-03-01');

INSERT INTO Employees (EmployeeID, EmployeeName, ProjectID, TaskID) VALUES
(1, 'Працівник 1', 1, 1),
(2, 'Працівник 2', 1, 2),
(3, 'Працівник 3', 1, 3),
(4, 'Працівник 4', 2, 4),
(5, 'Працівник 5', 2, 5);
SELECT
    P.ProjectID,
    P.ProjectName,
    E.EmployeeID,
    E.EmployeeName
FROM
    Projects P
LEFT JOIN
    Employees E ON P.ProjectID = E.ProjectID;
SELECT
    P.ProjectID,
    P.ProjectName,
    T.TaskID,
    T.TaskName,
    E.EmployeeID,
    E.EmployeeName
FROM
    Projects P
INNER JOIN
    Tasks T ON P.ProjectID = T.ProjectID
LEFT JOIN
    Employees E ON T.ProjectID = E.ProjectID AND T.TaskID = E.TaskID
WHERE
    P.ProjectID = 1;
SELECT
    AVG(DATEDIFF(DAY, GETDATE(), T.DueDate)) AS AverageDueDate,
    MAX(DATEDIFF(DAY, GETDATE(), T.DueDate)) AS MaxDueDate
FROM
    Tasks T;
