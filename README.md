# Database-Creation-and-Queries-with-PostgreSQL
## Table of Contents
- [Project Overview](#project-overview)
- [Project Introduction](#project-introduction)
- [Entity Relationship Diagram](#entity-relationship-diagram)
- [Metadata](#metadata)
- [Table Creation in PostgreSQL](#table-creation-in-postgresql)
- [Database Seeding](#database-seeding)
- [Queries for Business Questions](#queries-for-business-questions)
- [Summary](#summary)

### Project Overview
This project demonstrates core relational database and SQL skills. It involves designing a PostgreSQL database from the ground up using an Entity Relationship Diagram (ERD) as a blueprint.

Key components include:
- **ERD Design:** Created with diagramming tools to map out tables, relationships, and keys.
- **Database Setup:** Used SQL Data Definition Language (DDL) to define tables, primary/foreign keys, and structure.
- **Data Loading:** Applied Data Manipulation Language (DML) to insert and manage sample data.
- **Metadata Documentation:** Recorded attribute-level details such as data types, null constraints, and key roles.
- **Metadata Documentation:** Recorded attribute-level details such as data types, null constraints, and key roles.

### Project Introduction
Hermione's Hardware Store is a fictitious business that needs help with setting up a database to track its tool sales and rentals. Currently, the store owners are tracking everything with spreadsheets, but that is becoming cumbersome as business increases. After meeting with the store owners, enough information has been gathered to begin working on their new database system.

The store wants to keep records on a variety of business items and transactions. These include customer, tool, manufacturer, supplier, purchase, rental, and sale information. Tracking these items and transactions will enable the company to analyze different aspects of the business and make informed decisions.

The store owners need the database to adhere to several business rules:
- Each tool has a unique store identification number and a manufacturer serial number.
- The tools are made by the following manufacturers: Bosch, Craftsman, DeWalt, Dremel, Kobalt, Makita, Milwaukee, PorterCable, Rigid, Ryobi, Stanley, Hilt, Hitachi, Husky, and Bostitch.
- All tools are supplied by Supplier A, Supplier B, and Supplier C.
- The inventory can contain an unlimited number of tools.
- A customer can only rent up to three different tools at a time.
- The database needs to record the tools based on multiple features, including: manufacturer, supplier, area of use, power system, price, rental fee, insurance, etc.
- The database needs to be able to add new customers as needed.

### Entity Relationship Diagram
The Entity Relationship Diagram for the hardware store database is shown below. This shows all of the entities, their attributes, primary and foreign keys, and their relationships to each other. A customer can purchase and/or rent tools without having to set up an additional account.
![ERD](https://github.com/user-attachments/assets/83926a67-a357-47eb-9652-802fe4c878e4)

### Metadata
The nine entities, their attributes, and the primary keys are outlined below. These were developed with the business rules and requirements in mind. The primary keys are bolded, and the foreign keys are identified with “FK”. 


- *Tool:* **ToolID**, ToolName, ManuNo (FK), InventoryQty, UseArea, PowerSystem, RentalFee, SalePrice, PurchasePrice
- *Customer:* **CustomerID**, CustName, Phone, StreetAddress, City, State, ZipCode
- *Manufacturer:* **ManuNo**, ManuName
- *Supplier:* **SupplierID**, SupplierName, Phone, StreetAddress, City, State, ZipCode
- *Sale:* **SaleID**, CustomerID (FK), SaleDate, SaleSubtotal, SaleTax, SaleTotal
- *Sale_Tool:* **Sale_LineItem**, SaleID (FK), ToolID (FK), Quantity
- *Rent:* **RentID**, CustomerID (FK), RentDate, SaleSubtotal, SaleTax, SaleTotal
- *Rent_Tool:* **Rent_LineItem**, RentID (FK), ToolID (FK), CheckOutDate, ReturnDate, InsuranceFee, Status, LateFee
- *Supplier_Tool:* **SupplierToolID**, ToolID (FK), SupplierID (FK), OrderQuantity, Tax, Total

<img width="650" alt="Hardware_metadata" src="https://github.com/user-attachments/assets/343021e8-7d99-44db-84ce-cc103354007f" />

### Table Creation in PostgreSQL
These are the PostgreSQL statements to create the 9 tables in the database. Each table column is designated with data types and constraints (primary key, foreign key, not null, etc.)
![Table Creation Images](https://github.com/user-attachments/assets/4b900267-580f-4ab6-a1d6-bfb4ce753570)

### Database Seeding
I generated fictitious sample data to populate the tables. For brevity, only the *tool* table is shown below.
```SQL
INSERT INTO tool (toolid,toolname,serialno,inventoryqty,usearea,powersystem,
	rentalfee,saleprice,purchaseprice)
	VALUES
	(1001,'Wet/Dry Vacuum',46738,3,'floor','AC',20.00,100.00,60.00),
	(1002,'Leaf Blower',938006,3,'lawn & yard','battery',20.00,80.00,70.00),
	(1003,'Ladder',77336,5,'general','none',20.00,80.00,50.00),
	(1004,'Air Compressor',736559,4,'general','AC',40.00,200.00,150.00),
	(1005,'Air Nailer',54321,3,'construction','AC',30.00,120.00,70.00),
	(1006,'Carjack',84775,5,'auto','none',10.00,40.00,30.00),
	(1007,'Space Heater',457799,6,'general','AC',10.00,50.00,30.00),
	(1008,'Push Lawnmower',88473,4,'lawn & yard','fuel',30.00,150.00,120.00),
	(1009,'Riding Lawnmower',58844,3,'lawn & yard','fuel',60.00,1000.00,600.00),
	(1010,'Chainsaw',837267,3,'lawn & yard','fuel',20.00,100.00,60.00),
	(1011,'Carpet Shampoo',63746,6,'floor','AC',20.00,120.00,80.00),
	(1012,'Electric Sewer Snake',3009586,3,'plumbing','AC',30.00,100.00,60.00),
	(1013,'Manual Drain Cleaner',49586,4,'plumbing','none',10.00,50.00,40.00),
	(1014,'Generator',39958,3,'general','fuel',60.00,1000.00,600.00),
	(1015,'Table Saw',57687,3,'construction','AC',60.00,800.00,600.00),
	(1016,'Drain Camera',56978,2,'plumbing','AC',40.00,500.00,400.00),
	(1017,'Paint Sprayer',687934,3,'construction','fuel',30.00,100.00,60.00),
	(1018,'Shop Light',396887,4,'general','AC',20.00,100.00,60.00),
	(1019,'Garden Hose',45809,3,'lawn & yard','none',10.00,20.00,15.00),
	(1020,'Socket Set',30597,5,'general','none',10.00,100.00,60.00);
```

### Queries for Business Questions
Once the database structure was created and populated with data, it was ready for querying. The hardware store wants answers to some business questions, so let's query the database with PostgreSQL!
1. How many rental tools have a current status of “late”? What are the customers’ names and phone numbers for contacting them to remind them to return the tools?
   
![Query 1](https://github.com/user-attachments/assets/312855e6-d217-4c80-af31-6d12a075b41c)

2. The marketing department wants to know which three tools had the most sales in terms of quantity in January 2024 in order to prepare for advertisements for next January.
   
![Query 2](https://github.com/user-attachments/assets/7a1c64fd-3a2d-44c1-a7ef-10c6980e80b9)

3. Upon hearing that Supplier B may be going out of business, the store manager wants to determine which tools are provided by them so they can make arrangements to purchase those tools from a different supplier.

![Query 3](https://github.com/user-attachments/assets/10eb5365-1ec7-4ff5-b288-1e5124b52a28)

4. What is the total sales tax collected in the month of January 2024?

![Query 4](https://github.com/user-attachments/assets/f2af1b27-4774-483d-980e-29a10419c031)

5. Who are the top 10 customers in sales for the year 2024?

![Query 5](https://github.com/user-attachments/assets/29952785-6f0e-416e-8779-3055efceb038)

6. The rental manager is considering purchasing more tools. Which 3 tools were rented the most in 2024?

![Query 6](https://github.com/user-attachments/assets/f46566c8-e640-446d-ac56-73dde86ec709)

### Summary
Hermione's Hardware Store will benefit significantly from their new database. It enables more efficient data tracking while reducing reliance on spreadsheets. By streamlining operations, the database frees up time for other business priorities and supports data-driven decision-making. Additionally, it adheres to all business rules established by the store owners.
