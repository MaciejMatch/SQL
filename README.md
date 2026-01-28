# SQL Practice Repository :sparkles:

This repository contains my SQL practice work, including SQL scripts I have written and screenshots of query results.

The main goal of this repository is to document my learning process, demonstrate my SQL skills, and keep a structured collection of queries and results for future reference.

## Tool :hammer:

SQL Server Management Studio (SSMS) 2014

## Repository Content :pencil:
- SQL scripts with queries created during practice
- Screenshots presenting query results executed in SSMS
- Example databases and test cases used for learning and verification

## Purpose :rocket:
- Practice and improve SQL skills
- Showcase SQL queries and problem-solving approaches
- Keep evidence of query results for review and validation

## Exercises :arrow_down:

# Task 1 – Basic SELECT 

From the HumanResources.Department table, retrieve the DepartmentID and Name columns
```sql
Select DepartmentID,Name from HumanResources.Department;
```


![Task 1](https://drive.google.com/uc?export=view&id=1miapw5NKQK4JjlcrOdDgvbxjH3RyRf0F)
# Task 2 – Column Concatenation and Alias

From the Person.Address table, retrieve AddressID and a concatenation of the columns AddressLine1, City, and PostalCode:
- Between the values, first insert a comma followed by a space, and then a single space (format: address, city postalcode)
- Name the new column alias Adres
```sql
select AddressID, AddressLine1 + ', ' + City + ' ' +
PostalCode as Adres
from Person.Address;
```
 ![Task 2](https://drive.google.com/uc?export=view&id=1IuBfBPxDahHyPhz5rMZaWDt_Zzf8FPT5)
# Task 3 – Filtering with AND / OR

From the HumanResources.EmployeeDepartmentHistory table, return all records where:

- BusinessEntityID is greater than or equal to 200
- DepartmentID is equal to 6 or 4
```sql
Select BusinessEntityID from HumanResources.EmployeeDepartmentHistory
where BusinessEntityID >= 200
and (DepartmentID = 6 or DepartmentID=4);
```
![Task 3](https://drive.google.com/uc?export=view&id=1ragc93xJIy_Tm6UNsq4TD1hf6hJaS6PA)
# Task 4 – Filtering by Range and Date

From the HumanResources.EmployeePayHistory table, select the columns: BusinessEntityID,Rate,RateChangeDate Filter only those records where:
- Rate is between 60 and 100 and the rate change occurred no earlier than the year 2009
```sql
Select BusinessEntityID,Rate,RateChangeDate from HumanResources.EmployeePayHistory
- where Rate between 60 and 100 and RateChangeDate>='20090101';
```
![Task 4](https://drive.google.com/uc?export=view&id=1-rU0XSniHDs63IEKRV3KTRtpnxqojyTj)
# Task 5 – Highest Value

From the Production.Location table, retrieve LocationID, Name, and CostRate:

- Return only one record with the highest CostRate
```sql
select top 1 LocationID,Name,CostRate from Production.Location
 order by CostRate desc;
```
![Task 5](https://drive.google.com/uc?export=view&id=114hTnIfhCszmE7VLFjcZe1kNG999B9gV)
# Task 6 – Grouping and Aggregation
From the HumanResources.Employee table, group the data by: MaritalStatus,Gender:
- Return these columns and add another column that sums the differences between VacationHours and SickLeaveHours for each group
```sql
Select MaritalStatus,Gender,sum(VacationHours-SickLeaveHours) as "Do wykorzystania" 
from HumanResources.Employee
group by MaritalStatus,Gender;
```
![Task 10](https://drive.google.com/uc?export=view&id=1cOTl5uOd5wbSPqEKU6hHXtvSVxKvGj_a)
# Task 7 – String Functions
From the Person.CountryRegion table return: 
- the column Name
add a column named Alias, which is a combination of the first and last letter of the name, where:
- the first letter is lowercase
- the last letter is uppercase
- Add another column that:
-returns the full name if it is a single-word name, returns only the last word if the name consists of multiple words

```sql
select name, lower(Left(name,1)) + upper(right(name,1)) as
"Alias",
case when charindex(' ',name) = 0 then name
else right(name,charindex(' ',reverse(name))-1)
end as "Ostatnie słowo"
from Person.CountryRegion;
```
![Task 12](https://drive.google.com/uc?export=view&id=1zmP6Fx8DQnVQtIjMnwysZNZ1qhP8oisY)
# Task 8 – Joining Multiple Tables
Join the following tables:Person.BusinessEntityAddress, Person.Address, Person.AddressType.The result should include:
- BusinessEntityID
- address type name (Name)
- address (AddressLine1, PostalCode, City)
```sql
select B.BusinessEntityID, T.Name, A.AddressLine1,
A.PostalCode, A.city
from Person.BusinessEntityaddress as B inner join
person.address as A on B.AddressID=A.AddressID
inner join Person.AddressType as T on
b.AddressTypeID=T.AddressTypeID;
```
![Task 14](https://drive.google.com/uc?export=view&id=1w3l9J8_fUiwH2QFUx9I8mL8yT0UipBF5)
# Task 9 – LEFT JOIN and Sorting
Join the tables: HumanResources.Employee, HumanResources.JobCandidate Return:
- all records from JobCandidate
- only matching records from Employee
- From JobCandidate, return only JobCandidateID
- From Employee, return all columns
- Sort the results so that candidates who were hired appear at the top
```sql
select J.JobCandidateID,E.*
from HumanResources.Employee as E
right join HumanResources.JobCandidate as J
on E.BusinessEntityID=J.BusinessEntityID
order by E.BusinessEntityID desc;
```
![Task 15](https://drive.google.com/uc?export=view&id=1RAUFoYhJ23pod9i_yOQg8747KzW_URmp)




## Notes ⭐
All queries are executed and tested using SQL Server Management Studio 2014.  
Scripts may be adapted for other SQL engines if needed.
