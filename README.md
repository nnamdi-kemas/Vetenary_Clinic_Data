# Vetenary_Clinic_Data
![](https://github.com/nnamdi-kemas/Vetenary_Clinic_Data/blob/main/petpicture.PNG)

## Overview

I was required to assist a vertinary clinic make sense of their data. Their data is dispersed accross multiple CSV files and they needed me to perform the following analytics

1. Extract information on pet names and owners' names sids by side.
2. Find out which pets from this clinic had precedures performed.
3. Match up all procedures performed to the descriptions.
4. Extract a table of individual costs (procedure prices) incurred by owners of pets from the clinic in question (the table should have owner and procedure price side by side).

## Tool used
- MySQL

## Skills Demostrated
- Data extraction
- Joining
- Aggregation.

Here's a structured approach applied in accomplishing each of the tasks:

### Task 1: Extract Information on Pet Names and Owners' Names Side by Side
```sql
select pets.Name as "PetName", petowners.Name as "PetOwner", petowners.Surname from pets
inner join petowners
on pets.OwnerID = petowners.OwnerID;
```
![](petnameandowner.PNG)

This query joins the pets and owners tables to retrieve pet names and their corresponding owners' names side by side.

### Task 2: Find out Which Pets Had Procedures Performed

Query to Find Pets with Procedures:
```sql
select distinct pets.Name, pets.Kind, petprocedureshistory.ProcedureType from pets
inner join petprocedureshistory
on pets.PetID = petprocedureshistory.PetID;
```
![](https://github.com/nnamdi-kemas/Vetenary_Clinic_Data/blob/main/nameandproceduretype.PNG)
This query retrieves distinct pet names from the pets table that have entries in the procedures table.

### Task 3: Match Up All Procedures Performed to Their Descriptions
To match procedures performed to their descriptions, I simply queried the procedures table:

```sql
select ProcedureType, Description from petproceduresdetails;
```

This query will give you a list of all procedures performed along with their descriptions.

![](https://github.com/nnamdi-kemas/Vetenary_Clinic_Data/blob/main/proceduretypeanddescription.PNG)
## Task 4: Extract a Table of Individual Costs (Procedure Prices) Incurred by Owners
Assuming you want to extract a table showing owners and the total costs incurred for procedures for their pets.

Query to Calculate Total Procedure Costs Per Owner:

sql
Copy code
SELECT o.owner_name, SUM(pr.procedure_cost) AS total_cost
FROM owners o
JOIN pets p ON o.owner_id = p.owner_id
JOIN procedures pr ON p.pet_id = pr.pet_id
GROUP BY o.owner_name;
This query joins the owners, pets, and procedures tables, calculates the total cost of procedures for each owner's pets, and groups the results by owner name.

Conclusion
Make sure to import the CSV files into MySQL using appropriate commands (LOAD DATA INFILE or through MySQL Workbench), create the necessary tables with correct foreign key relationships, and execute the queries provided to perform the required analytics tasks. Adjust column names and data types as per your actual CSV file structures. This structured approach should help you effectively analyze the veterinary clinic's data using MySQL.






