# Database-Creation-and-Queries-with-PostgreSQL
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
