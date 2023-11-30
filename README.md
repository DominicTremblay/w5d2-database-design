# Database Design

## Agenda

- What is database design
- Entity-Relationship Diagrams
  - Entities and attributes
  - Relationships
  - Conventions
  - Primary and Foreign keys
- Hands-On Exercise
  - Creating the Movies DB ERD
  - [Movies DB Exercise](https://gist.github.com/DominicTremblay/826a607bf3f18d9a21858a1dd9115a07)
- Database Tables Recap
- Movies DB ERD solution
- Database Normalization

#### 1.1 What is Database Design

* Database design refers to the process of structurally defining the data storage, organization, and management in a database.

* It involves determining the entities, the attributes within these entities, and the relationships between entities.

* Good database design ensures data integrity and consistency while minimizing redundancy and potential for errors.

### 2. Entity-Relationship Diagrams (ERDs), Entities, and Attributes

*  An Entity-Relationship Diagram (ERD) is a visual representation of the entities within a database system and the relationships between these entities.

* Conceptual model independant of any physical implementation.

* The `schema` of the database is the logical representation of the ERD in a DBMS like Postgresql.

#### 2.1 Entities

- An entity in an ERD represents a real-world object or concept that can be distinctly identified and is relevant to the database.

- Each entity has attributes, which are properties or characteristics of the entity (e.g., a Customer entity might have Name, Address, Phone Number).

- It's akin to a noun in a language, such as a person (e.g., Customer), place (e.g., Store), thing (e.g., Product), or concept (e.g., Order).

#### 2.2 CUSTOMER ORDERS DEMO

* Demonstration of entities and attributes => ex.: customers, orders, products

- Customers can order products
- What are the entities?
- What are the attributes?
- What are the relationships?
- What is the cardinality?

- [ERD Exercise](https://gist.github.com/DominicTremblay/826a607bf3f18d9a21858a1dd9115a07)
- [Customer's Orders ERD](./images/customers_erd.png)

#### 2.3 Primary Key

* A way of uniquely identifying a particular record in a database table 
* Must be unique (within the table) and can never be null
* The usual data type is auto-incrementing integer (`INTEGER` or `BIGINT`)
* A Primary Key stored in another table is known as a `Foreign Key`
* The Primary Key and Foreign Key **MUST** be the same data type

#### 2.4 Naming Conventions

* Entity and attribute names are written in `snake_case`
* Entity names are always pluralized
* The primary key for each entity will simply be called `id`
* A foreign key is made up of the singular of the primary keys entity and the suffix `_id` (eg. `user_id` is the foreign key for the `id` attribute in the `users` entity)

### 2.5 Cardinality of Relationship

* **One-to-One**: One record in the first table is related to one (and only one) record in the second table
* **One-to-Many**: One record in the first table is related to one or more records in the second table
* **Many-to-Many**: One or more records in the first table are related to one or more records in the second table

* It could be argued that there is really only one relationship type: _One-to-Many_ as One-to-One's are extremely rare and Many-to-Many's are implemented using two _One-to-Many's_

### 3. **Tables in PostgreSQL**

   - Understanding the concept of tables in relational databases
   - Entities are tables. Tables are like spreadsheet
   - The table fields are columns
   - A record is a row

#### 3.1 Data Types

* Each field in a table **must** have a data type defined for it
* The data type tells the database how much room to set aside to store the value _and_ allows the database to perform type validation on data before insertion (to protect the data integrity of the table)
* Choosing the perfect data type is less of a concern nowadays because memory is now comparably cheap

##### 3.1.1 Main Data Types For Postgresql

* Boolean
* Character Types [VARCHAR(n), TEXT]
* Numeric Types [SMALLINT, INT, SERIAL, FLOAT(n)]
* Temporal Types [ DATE, TIME, TIMESTAMP ]

##### 3.1.2 Other types:

* UUID [ for storing UUID (Universally Unique Identifiers) ]
* Array [ for storing array strings, numbers, etc.]
* JSON [ stores JSON data]
* hstore [ stores key-value pair]
* Special Types [ such as network address and geometric data]

* [Data Types](https://www.geeksforgeeks.org/postgresql-data-types/)

### 4. Create the Movies DB ERD

- create the movies schema in [https://dbdiagram.io/](https://dbdiagram.io/)

OR

- [Draw.io - Movies DB ERD](https://draw.io)

#### Movies DB ERD

- [Draw.io - version](./images/movies_db_erd.png)
- [dbdiagram - version](./images/movies_db_erd_dbdiagram.png)


### 5. **Database Normalization** 

- Normalization is a systematic approach of decomposing tables to eliminate data redundancy(repetition) and to ensure data integrity. 

- Eliminating redundant(useless) data, therefore handling data integrity, because if data is repeated it increases the chances of inconsistent data.

- Normalization helps in keeping data consistent by storing the data in one table and referencing it everywhere else.

- [database normalization](https://www.studytonight.com/dbms/database-normalization.php)

#### 5.2 Normalization Exercise

When all the data is found in a single table, we have a few issues.

- [movies_directors.png](./images/movies_directors.png)

Issues:

- What if we want to create a director without a movie?
- Repetition of the director when they directed several movies
- What if an info is wrong such as the director's email?
- What if we assign the wrong director to several movies? 
- Director's name are not atomic

Solution: break down into several tables

