# HR Department Dashboard


## Problem Statement

###  Demographic Analysis and Impact of Location:

- What is the gender distribution across different departments?

- How does the racial composition vary by department and job title?

- What is the distribution of employees in different locations?

- How do the working conditions (e.g., average tenure, age distribution) vary between different locations?


### Hiring Trends:

- What are the trends in hiring over the years? (e.g., How many employees were hired each year?)
- Which departments have the highest and lowest hiring rates?


### Employee Retention:

- What is the average tenure of employees in different departments and job titles?

### Geographical Insights:

- How is the workforce distributed across different cities and states?
- Are there any significant differences in employee demographics based on location?

### Age and Tenure Analysis:

- What is the average age of employees at the time of hiring in different departments?

### Department and Job Title Analysis:

- What is the distribution of job titles within each department?
- Are there specific job titles that show higher turnover rates?


### Steps followed 

- Step 1 : Load data into SQL, dataset is a SQL file.
- Step 2 : Cleaned data and created problem-solving queries.
- Step 3 : Queries for each problem statement:
### Demographic Analysis and Impact of Location:

- What is the gender distribution across different departments?

        SELECT department AS Department, gender AS Gender, COUNT(*) AS Count
        FROM humanResources
        GROUP BY department, gender;
- How does the racial composition vary by department and job title?

        SELECT department AS Department, jobtitle AS Jobtitle, race AS Race, COUNT(*) as Count
        FROM humanResources
        GROUP BY department, jobtitle, race;

- What is the age distribution of employees in different locations?

        SELECT location AS Location, FLOOR(DATEDIFF(YEAR, birthdate, GETDATE()) / 10) * 10 AS Age_group, COUNT(*) AS Count
        FROM humanResources
        GROUP BY location, FLOOR(DATEDIFF(YEAR, birthdate, GETDATE()) / 10) * 10;


### Hiring Trends:

- What are the trends in hiring over the years? (e.g., How many employees were hired each year?)

        SELECT YEAR(hire_date) AS Hire_year, COUNT(*) AS Hires
        FROM humanResources
        GROUP BY YEAR(hire_date);

- Which departments have the highest and lowest hiring rates?

        SELECT department AS Department, COUNT(*) AS Hires
        FROM humanResources
        GROUP BY department;

### Employee Retention:

- What is the average tenure of employees in different departments and job titles?

        SELECT department AS Department, jobtitle AS Jobtitle, 
                AVG(DATEDIFF(DAY, TRY_CONVERT(DATE, hire_date), 
                                ISNULL(TRY_CONVERT(DATE, termdate), GETDATE()))) AS Average_tenure_days
        FROM humanResources
        GROUP BY department, jobtitle;

### Geographical Insights:

- How is the workforce distributed across different cities and states?

        SELECT location_city, location_state, COUNT(*) AS Count_of_Employee
        FROM humanResources
        GROUP BY location_city, location_state;

- Are there any significant differences in employee demographics based on location?

        SELECT location, gender, race, COUNT(*) AS Count_of_Employee
        FROM humanResources
        GROUP BY location, gender, race;

### Age and Tenure Analysis:

- What is the average age of employees at the time of hiring in different departments?

        SELECT department AS Department, AVG(DATEDIFF(YEAR, birthdate, TRY_CONVERT(DATE, hire_date))) AS Average_age_at_hire
        FROM humanResources
        GROUP BY department;

### Deparment and Job Title Analysis:

- What is the distribution of job titles within each department?

        SELECT department AS Department, jobtitle AS Jobtitle, COUNT(*) AS Count_of_Employee
        FROM humanResources
        GROUP BY department, jobtitle;

- Are there specific job titles that show higher turnover rates?

        SELECT jobtitle AS Jobtitle, COUNT(*) AS Turnover_count
        FROM humanResources
        WHERE termdate IS NOT NULL
        GROUP BY jobtitle;

- Step 4 : Saved this query and import it into PowerBI Desktop;
- Step 5 : Created an additional column for Tenure Days, also created DAX measures and Key measure table for all measurements:

        * Female Count = CALCULATE(COUNTROWS('humanResources'), 'humanResources'[gender] = "Female")
        * Male Count = CALCULATE(COUNTROWS('humanResources'), 'humanResources'[gender] = "Male")
        * Hiers Count = CALCULATE(COUNTROWS('humanResources'), NOT(ISBLANK('humanResources'[hire_date])))
        * Average Tenure Days = AverageTenureDays = AVERAGEX(humanResources,humanResources[TenureDays])
        
- Step 6 : Established Relationships between Data Models;
- Step 7 : Created Dashboard design for page "Demographic Analysis and Impact of Location".
- Step 8 : Visual filters (Slicers) were added for two fields named:

Department

![Slicer of Department](https://github.com/Tsukhishvili-Giorgi/HR-Department-Analyze/assets/117026869/e1f23c7b-378b-46a7-9538-0536194f5ba1)

Workspace Location

![Slicer of Workspace Location](https://github.com/Tsukhishvili-Giorgi/HR-Department-Analyze/assets/117026869/aefb118e-bc65-4353-bf25-cb63a0e406c0)


- Step 9 : Created three cards:

Male Count

![Male Count](https://github.com/Tsukhishvili-Giorgi/HR-Department-Analyze/assets/117026869/1faa6713-60dd-4c50-85de-167611373839)

Female Count

![Female Count](https://github.com/Tsukhishvili-Giorgi/HR-Department-Analyze/assets/117026869/f0f4b5b8-45d0-4883-ba76-157aa49846c7)

Average Tenure Days

![Average Tenure Days](https://github.com/user-attachments/assets/dfd24b7b-1580-450a-a0a4-e6bbd70cc24e)


- Step 10 : Created Clustered Bar and Pie charts to define race and job title count;

![Count By Jobtitle](https://github.com/Tsukhishvili-Giorgi/HR-Department-Analyze/assets/117026869/5978fd2d-79af-4dce-9e91-57e40b89d1ee)

![Count By Race](https://github.com/user-attachments/assets/54bf8768-a0c0-48e3-82af-4753a49a0328)

- Step 11 : Created Dashboard design for page "Hiring Trends".
- Step 12 : Created Slicer of Deparment and Card for Hires of Count.

![Card and Slicer](https://github.com/user-attachments/assets/b12e21b8-e9ca-41aa-8e9b-89a08e2ec93a)

- Step 13: Created Clustered Bar chart to define count of Hires by Department;

![Count of Hires By Department](https://github.com/user-attachments/assets/30375ce9-196b-45fb-b008-db18d07cb26f)

- Step 14 : A line chart used to show the year on year count of Hires:

![years on years count of hires](https://github.com/user-attachments/assets/f2c01706-62a6-42e9-ad25-0528e2deff0b)


- Step 15 : Created a Dashboard design for the page "Employee Retention".

- Step 15 : There are also created a Slicer of Department and Card for Count of Hire.

- Step 16 : Stacked bar charts are used to show Average Tenure Days by Jobtitle and department.

![AvgTenureDays By Jobtitle and Department](https://github.com/user-attachments/assets/ea303d0b-a454-4f7a-b44b-be1459c04449)

- Step 16 : Created Dashboard design for page "Geographical Insights".

- Step 17 : Created a Slicer of Race.

![Slicer of Race](https://github.com/user-attachments/assets/fbb9f8db-04fc-44b4-abef-eb350e5ffeb9)

- Step 18 : Created Clustered Bar chart to define count of Employees by Location and Gender;

![Count of Employee by Gender and Location](https://github.com/user-attachments/assets/1aa01425-3f42-4327-ab4c-6b44db2c482f)

- Step 19 : Create Map to define count of Employee by Location City and Location State;

![Employee by Location City and Location State](https://github.com/user-attachments/assets/4d5ac718-e7fa-41a9-afaf-7cac977cc329)

- Step 20 : Created Dashboard design for page "Age and Tenure Analysis".

- Step 21 : There are also created a Slicer of Department and two Cards for Count of Male and Female.

- Step 22 : Created a table to show the Average age at hire.

![Average age at Hire](https://github.com/user-attachments/assets/ff8585ca-424f-4646-948e-bb008a93bf0a)

- Step 23 : Created Dashboard design for the page "Department and Jobtitle Analysis".

- Step 24 : Created Slicer of Department.

- Step 23 : Created Clustered and Stacked Bar charts to define Turnover count by Jobtitle and Count of Employees by Jobtitle;

![Turnover Count By Jobtitle](https://github.com/user-attachments/assets/303f0531-02b7-47e6-bd31-05086a35efec) 

![Count of Emoloyee By Jobtitle](https://github.com/user-attachments/assets/0db5ad2c-de5e-40db-9bbc-f70abf44507e)


# Report Snapshot (Power BI DESKTOP)

## Demographic Analysis and Impact of Location

![Demographic Analysis and Impact of Location](https://github.com/user-attachments/assets/5bfe277d-7b14-4561-ac8b-6320decaa799)

## Hiring Trends

![Hiring Trends](https://github.com/user-attachments/assets/fe5a36e8-5298-4a00-8c1a-aaeeea8c504d)

## Employee Retention

![Employee Retention](https://github.com/user-attachments/assets/13355529-a24c-407e-957a-a9fd88c01a3c)

## Geographical Insights

![Geographical Insights](https://github.com/user-attachments/assets/b96c3443-93f7-4fe2-829f-653969f89f7f)

## Age and Tenure Analysis

![Age and Tenure Analysis](https://github.com/user-attachments/assets/0a16e33e-bb0f-445d-8a13-c28808d41938)

## Department and Jobtitle Analysis

![Department and Jobtitle Analysis](https://github.com/user-attachments/assets/faedffca-0758-4d7f-be8c-338892012e37)

# Insights

The following inferences can be drawn from the dashboard;


## [1] Demographic Analysis and Impact of Location

### What is the gender distribution across different departments?

 - Max Count of Males By Department is 3373 in Engineering.

 - Max Count of Females By Department is 3120 in Engineering.

 - Min Count of Males By Department is 28 in Audit.

 - Min Count of Females By Department is 24 in Audit.

### How does the racial composition vary by department and job title?

- White = 6328 (28,49 %)

- Two or more races = 3648 (16,42 %)

- Black or African American = 3619 (16,29 %)

- Asian = 3562 (16,03 %)

- Hispanic or Latino = 2501 (11,26 %)

- American Indian or Alaska Native = 1327 (5,97 %)

- Native Hawaiian or Other Pacific Islander = 1229 (5,53)

### What is the distribution of employees in different locations?

- From Headquarters = 16 264 [Male = 8487, Female = 7777]

- From Remote = 5345 [Male = 2801, Female = 2544]

### How do the working conditions (e.g., average tenure) vary between different locations?

- Average tenure days By Location: Headquarters = 4999, Remote = 5012.

           
## [2] Hiring Trends

### What are the trends in hiring over the years? (e.g., How many employees were hired each year?)

- The minimum number of employees was in 2000 and was 220 people.

- The maximum number of employees in 2018 was 1147 people.

### Which departments have the highest and lowest hiring rates?

- The highest employment rate is in the engineering department and is equal to 6686.

- The lowest employment rate is in the audit department and is equal to 52.

## Employee Retention

### What is the average tenure of employees in different departments and job titles?

- The average Tenure Days by department are 5042.

- The highest average tenure days in the audit department is 5435, but in particular (Office Assistant II in the Research Department) which is equal to 8219.

- The lowest average tenure days in the legal department in particular (Marketing Manager) and is equal to 4754.

## Geographical Insights

### How is the workforce distributed across different cities and states?

- The largest number of employees is in Cleveland in the state of Ohio - 16 871.

- The smallest number of employees in Ohio is in the city of Hamilton - 14.

## Age and Tenure Analysis

### What is the average age of employees at the time of hiring in different departments?

The average age of hire is 25-26 years.

## Department and Jobtitle Analysis

### What is the distribution of job titles within each department?

- Accounting - 3333;

- Audit - 52; 

- Business Development - 1642;

- Engineering - 6686;

- Human Resources - 1807;

- Legal - 311;

- Marketing - 494;

- Product Management - 641;

- Research and Development - 1084;

- Sales - 1832;

- Services - 1686;

- Support - 954;

- Training - 1692;

### Are there specific job titles that show higher turnover rates?

There are 4 jobtitles for which turnover rates are higher than 100. 

- Business Analyst - 134;

- Research Assistant II - 120;

- Human Resources Analyst II - 118;

- Research Assistent I - 104;
