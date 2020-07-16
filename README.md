# Pewlett-Hackard-Analysis

## Data Visualization Week 7 Challenge 

## Background
This week's lessons centered around HR data for a large company with a great deal of people aging into retirement.  6 csv files were provided as data to load into the 6 database tables created in PostgreSQL throughout the module for this week.  The data consists of employee information listed in various tables.  The database is built as shown below in the ERD (Fig.1) and then used as a base to demonstrate various SQL query techniques.  

Fig.1
![](images/Fig1.png) 

## Technical Analysis

### Resources
* PostgreSQL / pgAdmin4
* 6 csv files were provided containing various data

### Assumptions
* The 3 tables for Deliverable #1 are generated from the original 6 tables loaded with the csv data
  1. **Current** Employees born between 1/1/1952 and 12/31/1955 (does not contain the same hire date requirement as in the modules)
  2. Number of each title retiring (this is pulled from the aforementioned table)
  3. Number of current employees with each title (all employees, not just those retiring)
* **Current** Employees means a to_date = '9999-01-01'


### Technical Steps
After joining tables (employee, titles, salaries) and filtering to birth dates in 1952-1955 (Fig.2), the instructions in the challenge walk you through the use of partitioning the data to find and remove unwanted duplicate rows (Fig.3).  
This table is exported to the [Data directory](Data): [deliverable_one_b.csv](Data/deliverable_one_b.csv)

**Fig. 2:**<br>

![](images/Fig2.png)

**Fig.3:**<br>

![](images/Fig3.PNG)


However, there seems to be a limitation in this method.  This method will provide a list containing the most recent title of the employees born 1952-1955, but only a subset of these employees are current employees.  The list needs to be pared down to only current employees (titles.to_date = 9999-01-01).  However, this cannot be accomplished unless the to_date column is included in the SELECT statement.  When the to_date column is used instead of the from_date column as requested in the challenge instructions, the method works as intended (only showing **current** employees after the partitioning step).  Although, after testing a theory, I found that the same information can be obtained with a simple query without partitioning (Fig.4).  I have saved all tables in the 

**Fig.4:**<br>

![](images/Fig4.png)

The number of retiring employees by title is obtained with the SELECT COUNT query (Fig.5) on the table developed above.<br>
This table is exported to the [Data directory](Data):  [retirees_by_title.csv](Data/retirees_by_title.csv)

**Fig.5:**<br>

![](images/Fig5.PNG)

The number of all employees by title is obtained with the SELECT COUNT query (Fig.6) on the original titles table.  Again, denoting current employees by setting the to_date = 9999-01-01.  
This table is exported to the [Data directory](Data):  [all_emps_by_title.csv](Data/all_emps_by_title.csv)

**Fig.6:**<br>

![](images/Fig6.PNG)

For Deliverable #2, a list of **current** employees that are eligible for the Mentorship program, we use a similar INNER JOIN as above coupled with the WHERE statements to parse the table to the requested data (Fig.7).  
This table is exported to the [Data directory](Data): [mentorship.csv](Data/mentorship.csv)

**Fig.7:**<br>

![](images/Fig7.PNG)


## Results

The total number of **all current** employees is 240k, broken down by title as shown below in Fig.8.
This table is exported to the [Data directory](Data):  [all_emps_by_title.csv](Data/all_emps_by_title.csv)

**Fig.8:**<br>

![](images/Fig8.PNG)

The first method (with the partitioning) gives a total of 90k employees born between 1952 and 1955 broken down as shown below in Fig.9.
This table is exported to the [Data directory](Data):  [retirees_by_title.csv](Data/retirees_by_title.csv)

**Fig.9:**<br>

![](images/Fig9.PNG)

However, as discussed above, I believe this method is not acurate and we should look at only **current** employees (to_date = 9999-01-01).  My method (described above in Technical Steps Section) gives a total of 70k retirees broken down as shown below in Fig.10.
This table is exported to the [Data directory](Data):  [retirees_by_title_test.csv](Data/retirees_by_title_test.csv)

**Fig.10:**<br>

![](images/Fig10.PNG)

From the mentorship program table we can run a SELECT COUNT statement to get the number of employees that are available for the mentorship role.  

## Recommendations for Further Analysis

