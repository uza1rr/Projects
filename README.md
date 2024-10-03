Contents

[Introduction 2](#_Toc178342739)

[Mission & Objectives 3](#_Toc178342740)

[Table Structures 5](#_Toc178342741)

[Database Schema 9](#_Toc178342742)

[Data Sample 12](#_Toc178342743)

[Key SQL Queries 13](#_Toc178342744)

[Relationships and Joins 17](#_Toc178342745)

[Data Integrity and Constraints 20](#_Toc178342746)

[Potential Use Cases 26](#_Toc178342747)

[Conclusion 32](#_Toc178342748)

# Introduction

The Business Development Bank of Canada (BDC) is a Crown corporation wholly owned by the Government of Canada. This database project represents the design considerations and good design practices which would go in designing a database for a bank such as BDC. It aims to help how they manage and leverage data for business growth and client support. The aims are to transform the way the organization interacts with information, streamlining processes and enhancing decision-making capabilities.

The project is a thorough effort to centralize and optimize the data management infrastructure. It includes the design, development, and implementation of a database system which is tailored to meet the needs of the bank. This system is designed to integrate seamlessly with our existing workflows while introducing new capabilities for data analysis, reporting, and client relationship management. Key aspects of the project include:

- Creation of a normalized database structure
- Implementation of efficient data storage and retrieval mechanisms
- Creating SQL queries which are essential in its performance

Purpose of Creating This Database System

The primary purpose of creating this database system is to empower our organization with a powerful tool for data-driven decision making and improved client services. Specifically, the system aims to:

1. **Centralize Information**: Consolidate data from various sources into a single, coherent system, eliminating data silos and reducing redundancy.
2. **Enhance Efficiency**: Streamline data entry, retrieval, and reporting processes, saving time and reducing the potential for human error.
3. **Improve Data Quality**: Implement data validation and integrity checks to ensure the accuracy and reliability of stored information.
4. **Facilitate Analysis**: Provide robust querying capabilities and integration with analytics tools to derive meaningful insights from our data.
5. **Support Client Relations**: Enable better tracking of client interactions, needs, and history to improve service delivery and relationship management.
6. **Enable Scalability**: Design a flexible system that can grow and adapt to our organization's evolving needs and the changing business landscape.

By achieving these objectives, the The database will serve as a cornerstone for our organization's data strategy, driving innovation, improving operational efficiency, and ultimately contributing to our overall business success.This introduction sets the stage for the rest of your article, providing context about the project and its importance. You can follow this with more detailed sections about the database design, implementation process, features, and benefits as outlined in your project structure.

# Mission & Objectives

BDC has a mission statement which is the following,

**“Our mission is to support Canadian entrepreneurs by providing financing, capital and advisory services with a focus on small and medium sized enterprises.”**

It aims to cater to Canadian entrepreneurs and SMEs so that they may thrive and become resilient in the modern business world. BDC has multiple objectives such as,

“BDC aims to support Canadian entrepreneurs to build strong and resilient businesses and, in doing so, contribute to creating a more prosperous, competitive and inclusive Canada.”

It also aims to provide flexible financing solutions, offer expert advisory services, support sustainable business practices.

The database system aims to serve as a cornerstone for our organization's data strategy, driving innovation, improving operational efficiency, and ultimately contributing to our overall business success.

# Table Structures

For the database we created multiple tables, such as Client, Employees, Branch, Industries, Transaction, Loans, Services, and Surveys. This section will provide a detailed breakdown of each table in the database, explaining the columns, and their data types, and the relationships between tables through primary and foreign keys.

1\. Clients Table

The Clients table stores essential information about our business clients.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| ClientID | Integer | Primary Key | Unique identifier for each client |
| BusinessName | Varchar(100) | Not Null | Name of the client's business |
| ContactInfo | Varchar(255) |     | Contact information for the client |
| IndustryType | Varchar(50) |     | Type of industry the client operates in |
| DateJoined | Date |     | Date when the client joined our services |

- **Clients**: This table is the cornerstone of our database, holding essential information about our business clients. It allows us to maintain detailed records of each client's profile and track their engagement with BDC services.

2\. Loans Table

The Loans table tracks all loan-related information for our clients.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| LoanID | Integer | Primary Key | Unique identifier for each loan |
| LoanAmount | Decimal(15,2) | Not Null | Amount of the loan |
| InterestRate | Decimal |     | Interest rate for the loan |
| Term | Integer | Not Null | Duration of the loan in months |
| Status | ENUM | Not Null | Current status of the loan (e.g., Active, Paid, Defaulted) |
| ClientID | Integer | Foreign Key | References the Clients table |

- **Loans**: The Loans table manages all aspects of loan products offered to clients. It enables us to track loan amounts, terms, and statuses, providing a clear picture of our lending activities.

3\. Services Table

The Services table contains information about the services offered by BDC.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| ServiceID | Integer | Primary Key | Unique identifier for each service |
| ServiceName | Varchar(100) | Not Null | Name of the service |
| Description | Text |     | Detailed description of the service |
| Cost | Decimal(10,2) | Not Null | Cost of the service |

- **Services**: This table catalogs all services offered by BDC, including their descriptions and costs. It's vital for service management and pricing strategies.

4\. Employees Table

The Employees table stores information about BDC employees.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| EmployeeID | Integer | Primary Key | Unique identifier for each employee |
| Name | Varchar(100) | Not Null | Full name of the employee |
| Position | Varchar(50) | Not Null | Job title or position of the employee |
| DepartmentID | Integer | Foreign Key | References a Departments table (not shown) |
| HireDate | Date | Not Null | Date when the employee was hired |

- **Employees**: This table maintains our workforce data, including roles and hire dates. It is crucial for tracking employee involvement in transactions and branch management.

5\. Transactions Table

The Transactions table records all financial transactions within the BDC system.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| TransactionID | Integer | Primary Key | Unique identifier for each transaction |
| ClientID | Integer | Foreign Key | References the Clients table |
| EmployeeID | Integer | Foreign Key | References the Employees table |
| BranchID | Integer | Foreign Key | References the Branches table |
| ServiceID | Integer | Foreign Key | References the Services table |
| LoansID | Integer | Foreign Key | References the Loans table |
| Date | Date |     | Date of the transaction |
| Amount | Integer |     | Amount of the transaction |
| TransactionType | Varchar(100) |     | Type or category of the transaction |

- **Transactions**: Serving as a central hub, this table records all financial interactions within the BDC system. It links clients, employees, branches, services, and loans, allowing for comprehensive transaction tracking and analysis.

6\. Industries Table

The Industries table categorizes the different industries of our clients.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| IndustryID | Integer | Primary Key | Unique identifier for each industry |
| IndustryName | Varchar(100) | Not Null | Name of the industry |
| Description | Text |     | Detailed description of the industry |

- **Industries**: By categorizing client industries, this table enables us to analyze trends and tailor our services to specific sector needs.

7\. Branches Table

The Branches table contains information about different BDC branch locations.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| BranchID | Integer | Primary Key | Unique identifier for each branch |
| Location | Varchar(255) | Not Null | Physical location of the branch |
| ContactInfo | Varchar(255) |     | Contact information for the branch |
| ManagerID | Integer | Foreign Key | References the Employees table |

- **Branches**: The Branches table keeps track of our physical locations, including contact information and management structure. It's essential for analyzing performance across different geographical areas.

8\. Surveys Table

The Surveys table stores client feedback and survey responses.

| **Column Name** | **Data Type** | **Constraints** | **Description** |
| --- | --- | --- | --- |
| SurveyID | Integer | Primary Key | Unique identifier for each survey |
| ClientID | Integer | Foreign Key | References the Clients table |
| DateCompleted | Date | Not Null | Date when the survey was completed |
| Responses | Text |     | Stored responses to the survey questions |

- **Surveys**: The Surveys table captures valuable client feedback, allowing us to measure satisfaction and identify areas for improvement in our services.

This table structure provides a comprehensive framework for managing BDC's data needs, allowing for efficient storage, retrieval, and analysis of client information, financial transactions, services, and feedback. The use of primary and foreign keys ensures data integrity and enables complex queries across multiple tables.

# ER Diagram

Due to the tables and fields included in the tables, multiple relations can be established between the tables. An efficient schema that reflects the complex relationships between various entities in our business operations. In this section we will see an overview of the Entity-Relationship Diagram (ERD) and a brief explanation of each table's purpose.

Entity-Relationship Diagram (ERD)

The ERD visually represents the relationships between the tables in our database. It shows:

- Clients as the central entity, connected to Loans, Transactions, and Surveys.
- Transactions as a hub, linking Clients, Employees, Branches, Services, and Loans.
- Industries linked to Clients.
- Employees connected to Branches (via the ManagerID relationship).


The diagram uses crow's foot notation to indicate one-to-many relationships between entities.

Relationships:

- One client can have multiple loans, transactions, and surveys.
- Each loan is associated with one client; a client can have multiple loans.
- Central table linking clients, employees, branches, services, and loans.
- Employees are associated with transactions and can manage branches.
- Each branch has a manager (an employee) and is associated with transactions.
- Services are linked to transactions.
- Indirectly related to clients through the ‘IndustryType’ field in the Clients table.
- Each survey is associated with one client.

For specific types of relationships, we have;  
One-to-Many (1: N) Relationships:

\- Clients to Loans: One client can have multiple loans.  
\- Clients to Transactions: One client can be associated with many transactions.  
\- Branches to Employees: One branch can have multiple employees.

Many-to-One (N:1) Relationships:  
\- Transactions to Services: Many transactions can be associated with one service type.  
\- Loans to Employees: Many loans can be approved by one employee.

One-to-One (1:1) Relationships\*\*:

\- Clients to Surveys: Each client feedback survey is associated with one specific client.

# Key SQL Queries

For BDC’s day-to-day activities, it requires a lot of SQL queries which need to be run on a regular basis. For the sake of staying in the constraints of article length, we will only focus on a few. Queries enable efficient data retrieval, analysis, and reporting, crucial for decision-making and daily operations. Here are examples of important SQL queries which will be useful for BDC:

1\. Client Overview Query

sql

**SELECT** c.ClientID, c.BusinessName, c.IndustryType,

COUNT(**DISTINCT** l.LoanID) **AS** ActiveLoans,

SUM(l.LoanAmount) **AS** TotalLoanAmount,

COUNT(**DISTINCT** t.TransactionID) **AS** TransactionCount

**FROM** Clients c

**LEFT** **JOIN** Loans l **ON** c.ClientID = l.ClientID AND l.**Status** = 'Active'

**LEFT** **JOIN** **Transactions** t **ON** c.ClientID = t.ClientID

**GROUP** **BY** c.ClientID, c.BusinessName, c.IndustryType;

This query provides a comprehensive overview of each client, including their active loans and transaction activity. It supports:

- Client relationship management by offering a snapshot of client engagement
- Risk assessment by showing the total loan exposure per client
- Marketing initiatives by identifying clients with high transaction volumes but low loan uptake

2\. Loan Performance Analysis

sql

**SELECT** i.IndustryName,

AVG(l.LoanAmount) **AS** AvgLoanAmount,

AVG(l.InterestRate) **AS** AvgInterestRate,

COUNT(**CASE** **WHEN** l.**Status** = 'Defaulted' **THEN** 1 **END**) **AS** DefaultCount,

COUNT(\*) **AS** TotalLoans,

(COUNT(**CASE** **WHEN** l.**Status** = 'Defaulted' **THEN** 1 **END**) \* 100.0 / COUNT(\*)) **AS** DefaultRate

**FROM** Loans l

**JOIN** Clients c **ON** l.ClientID = c.ClientID

**JOIN** Industries i **ON** c.IndustryType = i.IndustryName

**GROUP** **BY** i.IndustryName

**ORDER** **BY** DefaultRate **DESC**;

This query analyzes loan performance across different industries. It supports:

- Risk management by identifying high-risk industries.
- Loan policy adjustments based on industry-specific default rates.
- Strategic planning for loan product development

# Data Integrity and Constraints

For a banking operations, data integrity has to be ensured as it is very crucial for the reliability and consistency of the database. We've implemented various constraints and triggers to maintain data accuracy and enforce business rules. Such as foreign keys, which are essential for maintaining referential integrity between related tables. They help prevent invalid data entry, maintain relationships between tables, and automate certain business processes, thereby improving the overall reliability and efficiency of our database operations.

# Potential Use Cases

The database is designed to support a wide range of business activities and decision-making processes. In this section we will outlines some potential use cases and scenarios that demonstrate the system's utility across various aspects of BDC's operations. Such as client relationship management, BDC can leverage this for personalized client engagement. The database enables BDC to tailor its services and communication based on comprehensive client profiles.

Another use is risk assessment and management, as they are the core for efficient use and performance for a bank. The database can provide industry-specific loan risk analysis so that BDC can assess loan risks across different industries to inform lending policies.

The data base can also help in performance monitoring and employee evaluation he database facilitates the creation of performance dashboards for branches and employees

This dashboard helps management evaluate employee and branch performance based on transaction volumes and client satisfaction.

And one of the main mission of BDC is to drive growth, identifying growth opportunities is also one of the potential use. The database can help BDC to make informed decisions about expanding services or opening new branches.

# Conclusion

The database system represents a significant milestone in the organization's journey towards data-driven decision-making and operational excellence. This comprehensive database solution has been meticulously designed and implemented to address the complex needs of our financial services operations, providing a robust foundation for growth, efficiency, and enhanced client service.

To summarize we designed and implemented a database that accurately reflects the relationships between key entities in our business ecosystem. Then we created a set of interconnected tables including Clients, Loans, Transactions, Employees, Branches, Services, Industries, and Surveys, each serving a crucial role in our data architecture. We then developed a series of SQL queries and join operations that enable deep insights into various aspects of our operations, from client relationship management to risk assessment. And lastly identified and outlined several potential use cases that demonstrate the system's utility across different business functions, showcasing its versatility and power.
