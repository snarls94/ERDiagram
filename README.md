# TechBank Database Design

This repository contains the database design proposal for **TechBank**, a modern banking institution offering a wide range of financial products and services. The goal of this project is to create an efficient, scalable, and secure database system that manages customers, accounts, transactions, loans, credit cards, and branches for the bank.

## Objective

The objective of this database design is to provide a comprehensive and optimized solution for TechBank, addressing the following:

- **Entity-Relationship Diagram (ERD)**: Visual representation of the key entities, relationships, and attributes involved in the database schema.
- **Normalization**: Apply normalization techniques to ensure data integrity, reduce redundancy, and optimize database performance (up to 3NF).
- **Tables and Relationships**: Define the database tables, keys, constraints, and relationships between entities.
- **Scalability**: Ensure that the database can accommodate future growth and expansion.
- **Data Governance**: Implement data governance policies and procedures to manage data effectively.

## ERD (Entity-Relationship Diagram)

The **ERD** illustrates the following key entities and their relationships:

- **Customer**: Represents bank customers with attributes like `Customer_ID`, `First_Name`, `Last_Name`, etc.
- **Account**: Represents customer accounts, including details like `Account_ID`, `Account_Type`, `Balance`, etc.
- **Transaction**: Represents financial transactions related to accounts.
- **Branch**: Represents branches of TechBank, including branch address and manager details.
- **Loan**: Represents loans issued to customers, including loan details like `Loan_Amount`, `Interest_Rate`, etc.
- **CreditCard**: Represents credit cards issued to customers, including card details and balance.
- **Employee**: Represents bank employees and their assignments to branches.

### ERD Diagram

The ERD can be visualized and edited using [draw.io](https://app.diagrams.net/) or [LucidChart](https://www.lucidchart.com/). The design can be opened directly from this repository.

## Database Schema

The database schema includes the following tables:

- **Customer**: Contains customer information.
- **Account**: Contains account details and is linked to the `Customer` table.
- **Transaction**: Contains transaction details and is linked to the `Account` table.
- **Branch**: Contains branch information.
- **Loan**: Contains loan details and is linked to the `Customer` table.
- **CreditCard**: Contains credit card details and is linked to the `Customer` table.
- **Employee**: Contains employee details and is linked to the `Branch` table.

### SQL Table Definitions

```sql
CREATE TABLE Customer (
  Customer_ID INT PRIMARY KEY,
  First_Name VARCHAR(100),
  Last_Name VARCHAR(100),
  Address VARCHAR(255),
  Phone_Number VARCHAR(15),
  Email VARCHAR(100),
  Date_of_Birth DATE,
  SSN CHAR(9) UNIQUE
);

CREATE TABLE Account (
  Account_ID INT PRIMARY KEY,
  Account_Type VARCHAR(50),
  Balance DECIMAL(10,2),
  Open_Date DATE,
  Customer_ID INT,
  FOREIGN KEY (Customer_ID) REFERENCES Customer(Customer_ID)
);

CREATE TABLE Transaction (
  Transaction_ID INT PRIMARY KEY,
  Account_ID INT,
  Transaction_Type VARCHAR(50),
  Amount DECIMAL(10,2),
  Date TIMESTAMP,
  Description TEXT,
  FOREIGN KEY (Account_ID) REFERENCES Account(Account_ID)
);

CREATE TABLE Branch (
  Branch_ID INT PRIMARY KEY,
  Branch_Name VARCHAR(100),
  Branch_Address VARCHAR(255)
);

CREATE TABLE Loan (
  Loan_ID INT PRIMARY KEY,
  Customer_ID INT,
  Loan_Type VARCHAR(50),
  Loan_Amount DECIMAL(10,2),
  Interest_Rate DECIMAL(5,2),
  Start_Date DATE,
  End_Date DATE,
  Payment_Terms TEXT,
  FOREIGN KEY (Customer_ID) REFERENCES Customer(Customer_ID)
);

CREATE TABLE CreditCard (
  Card_ID INT PRIMARY KEY,
  Customer_ID INT,
  Card_Type VARCHAR(50),
  Credit_Limit DECIMAL(10,2),
  Balance DECIMAL(10,2),
  Expiry_Date DATE,
  CVV CHAR(3),
  FOREIGN KEY (Customer_ID) REFERENCES Customer(Customer_ID)
);

CREATE TABLE Employee (
  Employee_ID INT PRIMARY KEY,
  First_Name VARCHAR(100),
  Last_Name VARCHAR(100),
  Job_Title VARCHAR(100),
  Branch_ID INT,
  FOREIGN KEY (Branch_ID) REFERENCES Branch(Branch_ID)
);
