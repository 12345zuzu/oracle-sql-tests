CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) NOT NULL UNIQUE
);

-- Create Roles table
CREATE TABLE Roles (
    RoleID INT PRIMARY KEY,
    RoleName VARCHAR(100) NOT NULL
);

-- Create UserRoles table (Join table)
CREATE TABLE UserRoles (
    UserID INT,
    RoleID INT,
    PRIMARY KEY (UserID, RoleID),
    FOREIGN KEY (UserID) REFERENCES Users(UserID),
    FOREIGN KEY (RoleID) REFERENCES Roles(RoleID)
);

-- Create Projects table
CREATE TABLE Projects (
    ProjectID INT PRIMARY KEY,
    ProjectName VARCHAR(100) NOT NULL,
    UserID INT,
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);

-- Create Tasks table
CREATE TABLE Tasks (
    TaskID INT PRIMARY KEY,
    TaskName VARCHAR(100) NOT NULL,
    ProjectID INT,
    AssignedUserID INT,
    FOREIGN KEY (ProjectID) REFERENCES zouzucreator(ProjectID),
    FOREIGN KEY (AssignedUserID) REFERENCES zouzou(UserID)
);
INSERT INTO Users (UserID, UserName, Email) VALUES (1, 'zouzou', 'usengazuzu@gmail.com');
INSERT INTO Users (UserID, UserName, Email) VALUES (2, 'eric', 'nzabonaeric@gmail.com');

-- Insert Roles
INSERT INTO Roles (RoleID, RoleName) VALUES (1, 'Admin');
INSERT INTO Roles (RoleID, RoleName) VALUES (2, 'Developer');

-- Insert UserRoles
INSERT INTO UserRoles (UserID, RoleID) VALUES (1, 1);
INSERT INTO UserRoles (UserID, RoleID) VALUES (2, 2);

-- Insert Projects
INSERT INTO Projects (ProjectID, ProjectName, UserID) VALUES (1, 'ZOUCREATOR', 1);
INSERT INTO Projects (ProjectID, ProjectName, UserID) VALUES (2, 'ERICAFFECTOR', 2);

-- Insert Tasks
INSERT INTO Tasks (TaskID, TaskName, ProjectID, AssignedUserID) VALUES (1, 'Task 1', 1, 1);
INSERT INTO Tasks (TaskID, TaskName, ProjectID, AssignedUserID) VALUES (2, 'Task 2', 2, 2);
UPDATE Users SET Email = 'ZOULOU.new@gmail.com' WHERE UserID = 1;

-- Update Project's Name
UPDATE Projects SET ProjectName = 'Updated ZOUCREATOR' WHERE ProjectID = 1;
DELETE FROM Users WHERE UserID = 2;

-- Delete a Task
DELETE FROM Tasks WHERE TaskID = 2;
SELECT u.UserName, r.RoleName
FROM Users u
JOIN UserRoles ur ON u.UserID = ur.UserID
JOIN Roles r ON ur.RoleID = r.RoleID;

-- Join Projects with Users
SELECT p.ProjectName, u.UserName
FROM Projects p
JOIN Users u ON p.UserID = u.UserID;

-- Join Tasks with Projects and Users
SELECT t.TaskName, p.ProjectName, u.UserName
FROM Tasks t
JOIN Projects p ON t.ProjectID = p.ProjectID
JOIN Users u ON t.AssignedUserID = u.UserID;
