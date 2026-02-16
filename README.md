# Hospital_Data Project
-- Create Database Hospital_Data Project


CREATE DATABASE Hospital_Data_Project ;
USE Hospital_Data_Project ;

-- To Create Data table has hospital_data

CREATE TABLE Hospital_data ( Hospital_Name VARCHAR(50),
Location  VARCHAR(50),
Department  VARCHAR(50),
Doctors_Count INT,
Patients_Count INT,
Admission_Date DATE,
Discharge_Date DATE,
Medical_Expenses decimal(10,2));


-- Inserted data into table                                                                  

SELECT * FROM Hospital_data;                 -- To get all data about Hospital_data          
DESC Hospital_data;                          -- To Know Data type

Hospital_Data_Project

 1. Total Number of Patients 
-- Write an SQL query to find the total number of patients across all hospitals

SELECT 
    SUM(Patients_count) AS Total_Patients
FROM
    Hospital_data;

 2. Average Number of Doctors per Hospital 
--  Retrieve the average count of doctors available in each hospital.

SELECT 
    Hospital_name, AVG(Doctors_Count) AS AVG_Doctors
FROM
    hospital_data
GROUP BY Hospital_Name;

 3. Top 3 Departments with the Highest Number of Patients 
--  Find the top 3 hospital departments that have the highest number of patients. 

-- Top 3 hospital departments that have the highest number of patients. 
SELECT 
    Hospital_name, Department, Patients_Count
FROM
    Hospital_data
ORDER BY Patients_Count DESC
LIMIT 3;

-- Only Top 3 Departments with the Highest Number of Patients
SELECT 
    Department, SUM(Patients_Count) AS Total_Patients
FROM
    Hospital_data
GROUP BY Department
ORDER BY Total_Patients DESC
LIMIT 3;

 4. Hospital with the Maximum Medical Expenses 
-- Identify the hospital that recorded the highest medical expenses. 

-- Hospital with highest medical expenses.
SELECT 
    Hospital_Name, Medical_Expenses
FROM
    Hospital_data
ORDER BY Medical_Expenses DESC
LIMIT 1;

-- Hospital with highest total medical expenses.
SELECT 
    Hospital_Name,
    SUM(Medical_Expenses) AS Total_Medical_Expenses
FROM
    Hospital_data
GROUP BY Hospital_Name
ORDER BY Total_Medical_Expenses DESC
LIMIT 1;

 5. Daily Average Medical Expenses 
--  Calculate the average medical expenses per day for each hospital.

SELECT 
    Hospital_Name,
    ROUND(AVG(Medical_Expenses / DATEDIFF(Discharge_Date, Admission_Date)),
            2) AS Daily_Avg_Expenses
FROM
    Hospital_data
GROUP BY Hospital_Name
ORDER BY Daily_Avg_Expenses DESC;

 6. Longest Hospital Stay 
--  Find the patient with the longest stay by calculating the difference between Discharge Date and Admission Date.

SELECT 
    *, DATEDIFF(Discharge_Date, Admission_Date) AS Stay_Duration
FROM
    Hospital_data
ORDER BY Stay_Duration DESC;


 7. Total Patients Treated Per City 
--  Count the total number of patients treated in each city. 

SELECT 
    Location AS City, SUM(Patients_Count) AS Total_Patients
FROM
    Hospital_data
GROUP BY Location;

 8. Average Length of Stay Per Department 
--  Calculate the average number of days patients spend in each department.

SELECT 
    Department,
    AVG(DATEDIFF(Discharge_Date, Admission_Date)) AS Average_Stay_Days
FROM
    Hospital_data
GROUP BY Department
ORDER BY Average_Stay_Days DESC;

 9. Identify the Department with the Lowest Number of Patients 
-- Find the department with the least number of patients. 

SELECT 
    Department, SUM(Patients_Count) AS Total_Patients
FROM
    Hospital_data
GROUP BY Department
ORDER BY Total_Patients ASC
LIMIT 1;

 10. Monthly Medical Expenses Report 
--  Group the data by month and calculate the total medical expenses for each month.

SELECT 
    DATE_FORMAT(Discharge_Date, '%Y-%m') AS Month,
    SUM(Medical_Expenses) AS Total_Medical_Expenses
FROM
    Hospital_data
GROUP BY DATE_FORMAT(Discharge_Date, '%Y-%m')
ORDER BY Month;

-- OR Second Way

SELECT 
    YEAR(Discharge_Date) AS Year,
    MONTH(Discharge_Date) AS Month,
    SUM(Medical_Expenses) AS Total_Medical_Expenses
FROM
    Hospital_data
GROUP BY YEAR(Discharge_Date) , MONTH(Discharge_Date)
ORDER BY Year , Month;
