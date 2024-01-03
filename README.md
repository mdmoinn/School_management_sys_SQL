# Intro on School Management System


## Project Overview

Consider a fictional School “ABC Public School” situated in Delhi-NCR. This school has classes from 6th standard to 10th standard but they have just started gathering all the school data in a database. Therefore, we have limited data for class 8th, 9th and 10th.
In this problem, the school management wants to input the data in database quickly and efficiently so that they will get quick and actionable insights as fast as possible.
You have been hired as a data scientist and it's your responsibility to not only create the database but also get actionable business insights for the stakeholders.


## Data Sources

School_management_data_set: The primary dataset used for this analysis is the "School_management_data_set.txt".


## Tools
- DB-fiddle/ MySQL:
	- Data Analysis


## Data preparation

In the initial data preparation stage, follwoing task were performed:
  - Data loading and defining constraints such as "Not null", "Default" & "Check"
  - Defining Primary keys & Foreign keys. 


### Exploratory Data Analysis

EDA invloved exploring the School management data to answer key questions, such as:

#### SCENARIO 1:
  - Consider the scenario when school management wants to evaluate which employee will get the next promotion based their time in school, their designation along with their performance (which they evaluate based on feedback from student or their parents.)
      - Identify the age of employee when they joined the school
      - Identify the time spent by employees in school grouped by their designation
      - Total number of feedbacks for an employee on employee id

#### SCENARIO 2:
  - School wants to determine if they have to divide a class to create more sections or they have to merge multiple sections into one based on their strength. (If there are too many students in class then it would create chaos in class while if there are less students then it will be wastage of resources for school).
    - Identify the total number of students by Class_Id and Student_Class

#### SCENARIO 3: 
  - School provides bus services to differt locations of Delhi-NCR for students. School management wants to optimize the bus services in a way that we get no seat left in buses and everybody gets picked up. Provide following stats for internal evaluation of school
    - Total number of students by each city

#### SCENARIO 4:
  - Consider the scenario that the school is hosting an annual event where they will be distributing the prizes to students for various things. For instance, best performer in studies or sports or arts or some extra - curricular activities.
    - Class 8A student from Gurgaon has been a stellar performer whole year.
    - Class 9A and 10B students from Delhi are fantastic musicians and just gave an outstanding performance in a national level event.
    - Professor from Gurgaon who are with us since 2006 and 2020 has been a fantastic duo to carry out the science projects on state level with school students and got prize from state CM. 

 
### Data Analysis
SQL queries utlized:

#### SCENARIO 1:

	- SELECT *, Employee_since - YEAR(Employee_Birthdate) as Joining_age FROM employee ORDER BY Joining_age DESC;
	- SELECT *, (Extract (YEAR FROM NOW()))-Employee_since as Time_spent FROM employee ORDER BY Time_spent DESC;
	- SELECT E.Employee_Id, E.Employee_Name, COUNT(R.Rating) as total_feedbacks FROM employee as E JOIN ratings as R ON E.Employee_Id = R.Employee_Id GROUP BY E.Employee_Id, E.Employee_Name ORDER BY total_feedbacks DESC;


#### SCENARIO 2:

	- SELECT Student_Class, Class_Id, COUNT(*) as Total_students FROM student GROUP BY Student_Class, Class_Id;

#### SCENARIO 3:

	- SELECT Student_City, COUNT(*) no_of_student FROM student GROUP BY Student_City;


#### SCENARIO 4:

	- SELECT Student_Name FROM student WHERE Class_Id = 8 AND Student_Class = "A" AND Student_City = "Gurgaon";
	- SELECT Student_Name FROM student WHERE (Class_Id = 9 AND Student_Class = 'A' AND Student_City = 'Delhi') OR (Class_Id = 10 AND Student_Class = 'B' AND Student_City = 'Delhi');
	- SELECT Employee_Name FROM employee WHERE Employee_designation = 'Professor' AND Employee_City = 'Gurgaon' AND Employee_since IN (2006, 2020);
 
### Results/Findings:

The analysis results are summarised as follows:

#### SCENARIO 1:
- Joining age of Sharda (Principal) - 42years & Saniya (Assistant) - 36years
- Maximum time spent by Assistant "Saniya" for about 23years
- 4 number of feedbacks recieved by Uday & Komal which were maximum
  
**Therefore based on analysis next promotion is due for Saniya**



#### SCENARIO 2:
**- There are 5 students in each class & class id, no need to create or merge any sections**



#### SCENARIO 3:
- Students in Delhi - 13, Gurgaon - 10 & Noida - 7 total = 30, currently there are 2 buses with 12pax capacity each. **Hence need to increase the mini van by 1 number to accomodate 6 more students**

 

#### SCENARIO 4:
- Stellar performer award winner - **Abhimanyu**
- Music award winners - **Abhilasha, Anushka, Sanyam & Sanya**
- Science project award winner - **Professor Priya & Professor Rajesh**




 
