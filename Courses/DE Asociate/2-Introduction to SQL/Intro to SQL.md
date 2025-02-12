# Introduction to SQL
## Databases
A database stores data. Let's imagine that we are in charge of storing and organizing data for a library. We might set up a database that holds information such as the data pictured here on patrons, books, and checkouts.<br>
This information is housed in objects called tables, with data organized into rows and columns. This database contains a patrons table, a books table, and a checkouts table.<br>

A relational database defines relationships between tables of data inside the database. For example, each of our library patrons might each be associated with several checkouts. Through these relationships, we can draw conclusions about data housed in separate tables in the same database, and answer questions such as "Which books did James check out during 2022?" or "Which books are checked out most often?"

![](20250113234705.png)

These tables might look similar to the way data is organized in spreadsheet applications such as Excel or Google Sheets, but databases are far more powerful than spreadsheets.<br>
Databases can store much more data, and storage is more secure due to encryption.<br>
Possibly the biggest advantage of a database is that many users can write queries to gather insights from the data at the same time.<br>


## Tables
Tables are organized into rows and columns; in the world of databases, rows are often referred to as records and columns as fields. A table's fields are limited to those set when the database was created, but the number of rows is unlimited.<br>

Table names should be lowercase and should not include spaces - we use underscores in place of spaces. And ideally, a table name would refer to a collective group (like "inventory") but it's also okay for the table to have a plural name (such as "products").<br>

A **record** is a row in a table. It holds data on an individual observation. Taking a look at the patrons table, we see that the table has four records: one for each of the patrons.
![](20250113235646.png)

A **field** is a column in a table. It holds one piece of information about all observations in the table. The "name" field in the patrons table lists all of the names of our library patrons.
Because field names must be typed out when querying a database with SQL, field naming is important: 
- Should be lowercase and should not involve spaces.
- A field name should be singular rather than plural.
- Two fields in a table cannot have the same name.
- Should never share a name with the table they are housed in so that it's clear in all cases whether a field or table is being referred to.
![](20250113235718.png)

==A **unique identifier**, sometimes called a "**key**,"== is a unique value which identifies a record so that it can be distinguished from other records in the same table. This value is very often a number.
In the patrons table, it makes sense to use the card_num field as the unique identifier for each patron, not the name field, because it's possible that as our little library grows, two patrons might have the same name.

Having more tables, each with a clearly marked subject, is generally better than having fewer tables where information about multiple subjects is combined.
Now, here's what our patrons and checkouts tables would look like if we tried to combine them. It's the same data, but much less clear because it now contains duplicate information.
While we can see that Izzy has two checkouts and Maham has none, the card_num column is no longer unique because of Izzy's multiple checkouts.

***Table topics should remain separate***.
![](20250114000718.png)

## Data
When a table is created, a data type must be indicated for each field. The data type is chosen based on the type of data that the field will hold - a number, text, or a date for example.
-  First, different types of data are stored differently and take up different amounts of storage space.
- Second, some operations only apply to certain data types. It makes sense to multiply a number by another number, but it does not make sense to multiply text by other text for example.

![](20250114001221.png)

- **Strings:** In programming, a "string" refers to a sequence of characters such as letters or punctuation. Some string data types can only hold short strings, such as a string up to 250 characters. Storing short strings in a small data type like this saves storage space. SQL's VARCHAR data type is more flexible and can store small or large strings
- **Integers:** store whole numbers, such as the years in the member_year column of the patrons table. SQL offers a few different data types for storing integers, depending on how big the numbers we'd like to store are. INT, a common SQL integer data type, can store numbers from less than negative two billion to more than positive two billion.
- **Floats:** store numbers that include a fractional part, such as the 2.05. SQL also offers several float data types depending on how many digits the numbers in the field are expected to be. The NUMERIC data type can store floats which have up to 38 digits total.

**Schemas** are often referred to as "blueprints" of databases. A schema shows a database's design, such as what tables are included in the database and any relationships between its tables. A schema also lets the reader know what data type each field can hold.<br>

The schema for our library database shows the VARCHAR data type is used for strings like book title, author, and genre. We can also see that the patrons table is related to the checkouts table, but not the books table.
![](20250114002039.png)


## Introducing Queries
We use SQL queries to uncover trends in website traffic, customer reviews, and product sales. Which products had the highest sales last week? Which products get the worst review scores from customers? How did website traffic change when a feature was introduced?<br>
SQL shines when an organization has lots of data with complex relationships.<br>

![alt text](image.png)

Keywords are reserved words used to indicate what operation we'd like our code to perform. The two most common keywords are SELECT and FROM.<br>
The SELECT keyword indicates which fields should be selected - in this case, the name field. <br>
The FROM keyword indicates the table in which these fields are located - in this case, the patrons table.<br>

The SELECT statement appears first, followed on the next line by the FROM statement. It's best practice to end the query with a semicolon to indicate that the query is complete. We also capitalize keywords while keeping table and field names all lowercase.<br>
In order to share our results, we can save the SQL code we have written so that our collaborators can use it to query the database themselves. <br>

![alt text](image-2.png)

To select multiple fields, we can list multiple field names after the SELECT keyword, separated by commas.<br>
What if we'd like to select all four fields in the patrons table? We could list out the four field names after the SELECT statement, but there's an even easier way: we can tell SQL to select all fields using an asterisk in place of the four field names.<br>

![alt text](image-3.png)

### Aliasing
Sometimes it can be helpful to rename columns in our result set, whether for clarity or brevity. We can do this using aliasing.<br>
The alias only applies to the result of this particular query; in other words, the field name in the employees table itself is still name rather than first_name.<br>

![alt text](image-4.png)

### Distinct
Some SQL questions require a way to return a list of unique values. To get a list of years with no repeat values, we can add the DISTINCT keyword before the year_hired field name in the SELECT statement. Now, we can see that all of our employees were hired in just four different years.<br>

![alt text](image-5.png)

It's possible to return the unique combinations of multiple field values by listing multiple fields after the DISTINCT keyword.<br>
Take a look at the employees table. Perhaps we'd like to know the years that different departments hired employees. We could use this SQL query to look at this information, selecting the dept_id and year_hired from the employees table.<br>
Looking at the results, we see that department three hired two employees in 2021.<br>

![alt text](image-6.png)

To avoid repeating this information, we could add the DISTINCT keyword before the fields to select. Notice that the department id and year_hired fields still have repeat values individually, but none of the records are the same: they are all unique combinations of the two fields.

![alt text](image-7.png)

### Views
In SQL, a view refers to a table that is the result of a saved SQL SELECT statement. Views are considered virtual tables, which means that the data a view contains is not generally stored in the database.<br>
Rather, it is the query code that is stored for future use. A benefit of this is that whenever the view is accessed, it automatically updates the query results to account for any updates to the underlying database.<br>

To create a view, we'll add a line of code before the SELECT statement: CREATE VIEW, then the name we'd like for the new view, then the AS keyword to assign the results of the query to the new view name.<br>
`There is no result set when creating a view.`<br>

![alt text](image-8.png)

Once a view is created, however, we can query it just as we would a normal table by selecting FROM the view.<br>

![alt text](image-9.png)