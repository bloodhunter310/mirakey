# MySQL DB

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- MySQL
- MySQL Workbench
- SQL
- Connecting To MySQL
- Creating Schema
- SQL Queries

## MySQL

MySQL is a relational database management system that is based on SQL (structured query language). MySQL stores data in tables that consist of columns and rows.

### MySQL Installation

Download MySQL from this [link](https://dev.mysql.com/downloads/installer/) and run the installer, continue the installation process and make sure to include MySQL workbench, MySQL shell, and MySQL server. If the `mysql` command is not recognized as a command after the installation, make sure to add `mysql` to the operating system's environment variables.

### Running MySQL

Run MySQL workbench to use MySQL or run `mysql -u root -p` then enter the password to use MySQL from the terminal.

### SQL

Structured query language (SQL) is used to store and manipulate data in the database. It is used with MySQL and other SQL based databases and learning it is the first step of learning how to use these DBMSs.

Examples on SQL:

```sql
-- this is a comment in SQL

-- display databases
SHOW DATABASES;

-- create a database
CREATE DATABASE db_name;

-- delete a database
DROP DATABASE db_name;

-- select a database
USE db_name;

-- show tables
SHOW TABLES;

-- create a table (will create a table in the selected database)
-- AUTO_INCREMENT: the value gets incremented by 1 with every new record
-- NOT NULL: required
-- VARCHAR: a variable length string
-- other datatypes: https://www.w3schools.com/sql/sql_datatypes.asp
CREATE TABLE users (
    id INT AUTO_INCREMENT NOT NULL,
    name VARCHAR(255),
    age INT,
    email VARCHAR(255),
    country VARCHAR(255),
    city VARCHAR(255),
    created_at DATETIME,
    is_deleted TINYINT DEFAULT 0,
    -- primary key must be unique for each record and there must be only one primary key
    PRIMARY KEY (id)
);

-- show table information columns and rows
DESCRIBE table_name;

-- delete a table
DROP TABLE table_name;

-- insets (creates) a new row in the table `users` with the specified values
INSERT INTO users (name, email, country, city) VALUES ('John', 'john-doe@gmail.com', 'Italy', 'Rome');

-- selecting (retrieving) rows with  all columns (*) from the table `users`
SELECT * FROM users;

-- select rows with the columns (name, email) from the table `users`
SELECT name, email FROM users;

-- select rows with all columns from the table `users` that has the email set to john-doe@gmail.com
SELECT * FROM users WHERE email='john-doe@gmail.com';

-- select rows with all columns from the table `users` that has the country set to Italy and city to Rome
SELECT * FROM users WHERE country='Italy' AND city='Rome';

-- select rows with all columns from the table `users` that has the country set to Germany or France
SELECT * FROM users WHERE country='Germany' OR country='France';

-- select rows with all columns from the table `users` that has the country set to anything other than France
SELECT * FROM users WHERE NOT country='France';
```

## NodeJS-MySQL

To use MySQL with NodeJS install `mysql2` by using the following command `npm i mysql2` and require `mysql2` to be able to use it.

### Connecting MySQL

NodeJS can be connected to the database by using the `createConnection` method from `mysql2`.

```.env
DB_HOST=localhost
DB_USER=root
DB_PASS=secret
DB_NAME=db_name
```

```js
const mysql = require("mysql2");

const connection = mysql.createConnection({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASS,
  database: process.env.DB_NAME,
});

connection.connect((err) => {
  if (err) {
    console.error("error connecting: " + err.stack);
    return;
  }
  console.log("connected as id: " + connection.threadId);
});
```

### MySQL Schema

When dealing with MySQL it is possible to create a separate `.sql` file that contains the schema and can be executed (to create the schema) from the terminal by using the following command `mysql -u root < "file_name.sql" -p`. Make sure to enter the database password after that command.

An example of a MySQL schema:

```sql
USE db_name;

CREATE TABLE users (
    id int AUTO_INCREMENT NOT NULL,
    name varchar(255),
    email varchar(255),
    country varchar(255),
    city varchar(255),
    created_at DATETIME,
    is_deleted TINYINT DEFAULT 0,
    PRIMARY KEY (id)
);
```

### Running SQL Queries

To run SQL queries use the connection method `query`.

An example on running SQL queries:

1. db.js

   ```js
   const mysql = require("mysql2");

   const connection = mysql.createConnection({
     host: process.env.DB_HOST,
     user: process.env.DB_USER,
     password: process.env.DB_PASS,
     database: process.env.DB_NAME,
   });

   connection.connect((err) => {
     if (err) {
       console.error("error connecting: " + err.stack);
       return;
     }
     console.log("connected as id " + connection.threadId);
   });

   module.exports = connection;
   ```

2. test.js

   ```js
   // require the connection so it can be used
   const connection = require("./db");

   // query without placeholders
   const findJohn = () => {
     const query = `SELECT * FROM users WHERE name = "John"`;
     // use the query method to execute a query
     connection.query(query, (err, result, fields) => {
       if (err) throw err;
       // result are the data returned by mysql server
       console.log(result);
       // fields are extra meta data about result
       console.log(fields);
     });
   };

   // query with placeholders
   // it is recommended to use placeholders when dealing with user input variables to protect against
   // sql injection attacks done by the users
   const findUserByNameAndCity = (name, city) => {
     const query = `SELECT * FROM users WHERE name = ? AND city =?`;
     const data = [name, city];
     connection.query(query, data, (err, results) => {
       console.log(results);
     });
   };

   findJohn();
   findUserByNameAndCity("John", "Rome");

   const addUser = (user) => {
     const query = `INSERT INTO users (Name, email, country, city) VALUES (?, ?, ?, ?)`;
     const data = [user.name, user.email, user.country, user.city];
     connection.query(query, data, (err, results) => {
       console.log(results);
     });
   };

   const user = {
     name: "Stefan",
     email: "stefan@email.com",
     country: "Germany",
     city: "Berlin",
   };

   addUser(user);
   ```

### Pulse Check

0. Install MySQL server and workbench, and add `mysql` command to environment variables (if it doesn't already exist).

1. In the command line or MySQL workbench do the following:

   - Create a new Database `library`.
   - Use the newly created database.
   - Create a `books` table with the following columns: `title`, `author`, `published_at`, and `price` with the correct data types.
   - Insert five new rows into the `books` table.
   - Retrieve all rows from `books`.
   - Retrieve all books for a specific author by using the `WHERE` SQL statement.
   - Update the price for one of the books by using the `UPDATE` SQL statement.
   - Delete a book depending on the title by using the `DELETE` SQL statement.

2. Create a basic server without any APIs and connect the app to MySQL by using `mysql2`.

3. Create an API with the endpoint of `/books` that will insert a new book into the database.

4. Create an API with the endpoint of `/books` that will retrieve all books from the database.

### Practice

1. Create an API with the endpoint of `/books:book_id` that will update a book from the database.

2. Create an API with the endpoint of `/books:book_id` that will delete a book from the database.

3. Create a function that returns all books ordered in a descending order. Read about `ORDER BY`

4. Insert a book with a `null` value for the `price` column then create a function that returns all books that don't have a price. Read about `IS NULL`.

5. Create a function that returns all books that have a price.
