# Library-Database

MiniWorld Description: LIBRARY database 

Consider a library database in which the library records information about customers who borrow books (i.e loans made by the library), books the library stores, loans made, authors, publishers, and fines associated with the loans. The data requirements are summarized as follows:

*  The library has customers which are members of the library, each of whom is identified by a unique customer number and is described by their first name, last name, phone number, email ID, and address
* The library contains various books which are identified by a unique book number, the title of the book, the author ID, publisher ID, ISBN number, and genre 
* The authors are identified by their unique author number, first name, and last name 
*   The publishers are identified by their unique publisher number, first name, last name, year published, and book ID
*   Loans are created when customers borrow books which are identified by a unique loan number, the date the book was borrowed and is due, the customer who borrowed the book, the book that was borrowed, and the fine associated with the loan, if any

Description of entities and attributes 

The baseline conceptual model should contain the following <entity;attributes>;

1. <customers; Customer_ID (PK), First_Name, Last_Name, Phone_Number, Email_ID, Address>
2. <authors; Author_ID (PK), First_Name, Last_Name>
3. <publishers; Publisher_ID (PK), Publisher_Name, Year_Published>
4. <books; Book_ID (PK), Title, Author_ID (FK), Publisher_ID (FK), ISBN_Number, Genre>
5. <loans; Loan_ID (PK), Borrowed_Date, Due_Date, Borrower_ID (FK), Book_ID (FK), Fine>

Description and correct mapping of all relationships 

The minimum conceptual model should have the following relationships and cardinalities

1. Each customer makes zero or many (0, N) loans
2. Each loan can have one and only one (1, 1) customer 
3. Each loan made can have one and only one (1, 1) book 
4. Each book can have zero or many (0, N) loans
5. Each book can have one and only one (1, 1) author 
6. Each author can have one or many (1, N) books
7. Each book can have one and only one (1, 1) publisher 
8. Each publisher can publish one and many (0, N) books

Description and correct mapping of contraints related to business rules

The state of the library datatbase corresponds to the statuses of all its relations in a particular point in time 

The constraints are derived from the rules in the miniworld that the database represents 

Examples of constraints related to business rules

1. Inherent model-based (or implicity) constraints: 

*   the tuples are ordered i.e. the order of data insertion must be maintained
*   the tuples are heterogenous i.e. the tuples can consist of various data types 
*   each value in the tuple is atomic i.e. it is not divisible into components 
*   NULL values indicate either value unkown, value exists but is not available, or attribute does not apply to this tuple or value undefined

2. Schema-based (or explicity) constraints: 

Entity integrity constraints: no primary key value can be NULL

Primary Keys 

*   customers Table: Customer_ID
*   authors Table: Author_ID 
*   publishers Table: Publisher_ID 
*   books Table: Book_ID 
*   loans Table: Loan_ID 

Referential integrity constaints: between two relations, used to maintain the consistency among tuples in two relations. a tuple in one relation that refers to another relation must refer to an existing tuple in that relation

Foreign Keys: links the referencing relation to the referenced relation 

1. books Table: 
*   Author_ID in the books Table is a foriegn key refrencing Author_ID from the author Table
*   Publisher_ID in the publishers Table is a foreign key referencing Publisher_ID from the publishers Table

2. loans Table: 
*    Borrower_ID in the loans Table is a foreign key referencing Customer_ID in the customers Table
*   Book_ID in the loans Table is a foreign key referencing Book_ID in the books Table

3. Application-based (or semantic constraints): business rules that cannot be directly expressed in the schemas of the data model and must be enforced by the application programs 

these constraints are portrayed through the triggers created and are specific to the database of the miniworld

example 1: before inserting a new customer into the customers table - a trigger is needed to check if the customer already exists 

example 2: before updating a row in the customers table - a trigger is needed to check if the customer_ID can be changed

example 3: before deleting rows from the customers table - a trigger is needed to check for foreign key violations 

example 4: after deleting rows from the customer table - a trigger is needed to log the information about which customer was removed in the customers_log table 

Table creation and data loading, including relational constraints (PK, FK, NOT NULL)

The data for the library miniworld database was created in Excel. A new excel workbook is used for each entity. The data for each attribute of that entity is manually entered in Excel with the columns representing attribute names and the rows having the relevant data. 
Each Excel file for each entity is saved as a CSV file with the table name.

The CSV files are uploaded into Google Collab in the files section. Tables are created in Python by retrieving the data from the CSV files and are stored in library.db

The tables are made SQL compatible using .to_sql

Since the data was creating in CSV files, when library.db is downloaded and opened in DB browser for SQLite the constraints related to business rules are not directly displayed in the Database Structure Schema. However, for each table schema assume the following constraints:

1. authors Table:

Author_ID: PK, NOT NULL

First_Name: NOT NULL 

Last_Name: NOT NULL 

2. books Table:

Book_ID: PK, NOT NULL

Title: NOT NULL

Author_ID: NOT NULL, FK 

Publisher_ID: NOT NULL, FK

ISBN_Number: NOT NULL

Genre: no constraints 

3. customers Table:

Customer_ID: PK, NOT NULL 

First_Name: NOT NULL 

Last_Name: NOT NULL 

Phone_Number: no constraints 

Email ID: no constraints 

Address: no constraints

4. loans Table:

Loan_ID: PK, NOT NULL 

Borrower_Date: NOT NULL 

Due_Date: NOT NULL

Borrower_ID: NOT NULL, FK

Book_ID: NOT NULL, FK

Fine: NOT NULL 

5. publishers Table

Publisher_ID: PK, NOT NULL

Publisher_Name: NOT NULL

Year_Published: NOT NULL
