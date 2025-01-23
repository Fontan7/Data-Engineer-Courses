![[Pasted image 20250114194614.png]]

## Order of Execution
Unlike many programming languages, SQL code is not processed in the order it is written. Consider we want to grab a coat from a closet: first, we need to know which closet contains the coats. This is similar to the FROM statement, which is the first line to be processed. Before any data can be selected, the table from which the data will be selected needs to be indicated. Next, our SELECTion is made. Finally, the results are refined. Here we use the LIMIT keyword that limits the results to a specified number of records.
![[Pasted image 20250114201014.png]]
Also when where is present:
![[Pasted image 20250115000442.png]]
## Formatting
SQL is a generous language when it comes to formatting. New lines, capitalization, and indentation are not required in SQL as they sometimes are in other programming languages.
Over time, SQL users have developed style standards that are generally accepted across industries.

![[Pasted image 20250114203941.png]]

While keyword capitalization and new lines are standard practice, many of the finer details of SQL style are not. For instance, some SQL users prefer to create a new line and indent each selected field when a query selects multiple fields, as the query on this slide does.
Because of the different formatting styles, it's helpful to follow a SQL style guide, such as Holywell's, which outlines a standard of best practices for indentation, capitalization, and naming conventions for tables, fields, and aliases. Remember, though, that there is no single required formatting in SQL: the guiding principle is writing clear and readable code.
However, including a semicolon **;** at the end of the query is considered best practice for several reasons. First, some SQL flavors require it, so it's a good habit to have. Including a semicolon in a PostgreSQL query means that the query is more easily translated to another flavor if necessary. Additionally, like a period at the end of a sentence, a semicolon at the end of a query indicates its end, which is helpful in a file containing several queries.

While we can ensure our code is formatted beautifully, we don't have control over other people's SQL style. When creating a table, a SQL mistake is including spaces in a field name. To query that table, we'll need to enclose the field name in double-quotes to indicate that, despite being two words, the name refers to just one field.

## Filtering / WHERE
To filter, we need to use a new clause called WHERE, which allows us to focus on only the data relevant to our business questions.
We will be using comparison operators such as greater than. Here is an example of a query where we filtered to see only films released after the year 1960 using the greater than operator.
![[Pasted image 20250114235605.png]]

WHERE and the comparison operator, equals, can also be used with strings. In these cases, we will have to use single 'quotation' marks around the strings we want to filter.
Here is a final example that isn't as intuitive as the others. If we wanted to filter films to see all releases EXCEPT those from the year 1960, we would combine the less than and greater than symbols as shown here. This is the SQL standard symbol that means "not equal to".
![[Pasted image 20250114235830.png]]
![[Pasted image 20250115000108.png]]

We will be learning about three additional keywords that will allow us to enhance our filters when using WHERE by adding multiple criteria. These are OR, AND, and BETWEEN.
- OR: is used when we want to filter multiple criteria and only need to satisfy at least one condition.
- AND: If we want to satisfy all criteria in our filter, we need to use AND with WHERE.
- AND, OR: Let's kick it up a notch. We now want to filter films released in 1994 OR 1995, AND with a certification of either PG or R. Thankfully, we can combine AND and OR to answer this question. If a query has multiple filtering conditions, we will need to enclose the individual clauses in parentheses to ensure the correct execution order.
- BETWEEN: provides a valuable shorthand for filtering values within a specified range. This second query is equivalent to the one on the left. It's important to remember that BETWEEN is inclusive, meaning the results contain the beginning and end values.
![[Pasted image 20250115001930.png]]
![[Pasted image 20250115002436.png]]
![[Pasted image 20250115002623.png]]

#### LIKE, NOT LIKE and IN
- LIKE: We can use the LIKE operator with a WHERE clause to search for a pattern in a field. We use a wildcard as a placeholder for some other values to accomplish this. There are two wildcards with LIKE, the percent, and the underscore. The percent wildcard will match zero, one, or many characters in the text.
![[Pasted image 20250115005141.png]]

- NOT LIKE: We can also use the NOT LIKE operator to find records that don't match the specified pattern.
![[Pasted image 20250115005223.png]]

- IN: The IN operator allows us to specify multiple values in a WHERE clause, making it easier and quicker to set numerous OR conditions.
![[Pasted image 20250115005048.png]]

Its also important to understand the wildcard positions ( _ and %). We've reviewed one example of where to position each wildcard, but we can actually put them anywhere and combine them! We can find values that start, end, or contain characters in any position, as well as find records of a certain length. For example, this code on the left will find all people whose name ends in r. The code on the right will find records where the third character is t.
![[Pasted image 20250115005424.png]]


## COUNT() 
The COUNT function lets us do this by returning the number of records with a value in a field. If we want to count more than one field, we need to use COUNT multiple times.
![[Pasted image 20250114194946.png]]
Using COUNT with a field name tells us how many values are in a field. However, if we want to count the number of records in a table, we can call COUNT with an asterisk. The asterisk represents all fields. Passing the asterisk to COUNT is a shortcut for counting the total number of records.
Often, our results will include duplicates. We can use the DISTINCT keyword to select all the unique values from a field.

Combining COUNT with DISTINCT is also common to count the number of unique values in a field. This query counts the number of distinct birth dates in the people table. Some people in our table likely share the same birthday; COUNT would include all the duplicates while DISTINCT counts all of the unique dates, no matter how many times they come up.
![[Pasted image 20250114195534.png]]


## Summarizing Data
![[Pasted image 20250115230223.png]]

One way to do this is to summarize the data using SQL's aggregate functions. An aggregate function performs a calculation on several values and returns a single value.
We already know one aggregate function, COUNT()! These aggregate functions come after SELECT, exactly like COUNT(). We'll now learn four new aggregate functions.
- The SUM() function returns the result of adding the values in the a field.
- The MIN() function returns the lowest value of  a field.
- the MAX() function returns the highest value of a field.
- The AVG() function returns the average value of a field.

Although these functions appear to be mathematical, we can use several of them with both numerical and non-numerical fields. Average and sum are the two aggregate functions we can only use on numerical fields since they require arithmetic.
We can use count, minimum, and maximum with non-numerical fields.

`Remember data will only show for fields with valid/non NULL.`

We can combine aggregate functions with the WHERE clause to gain further insights from our data. That's because the WHERE clause executes before the SELECT statement.
![[Pasted image 20250115232940.png]]

#### ROUND()
In SQL, we can use ROUND() to round our number to a specified decimal. There are two parameters for ROUND(): the number we want to round and the decimal place we want to round to. Here we have re-calculated the same average budget as before, but this time we have included ROUND() and specified we want to round to two decimal places because we are dealing with currency.
The second parameter in our ROUND() function is optional, so we can leave it out if we want to round to a whole number. We would get the same result if we passed zero as the second argument, as it is the default when no number is given.
![[Pasted image 20250115233234.png]]

Here is a tricky one: we could also pass a negative number as the second parameter and still get a result. Here, the function is rounding to the left of the decimal point instead of the right. Using negative five as the decimal place parameter will cause the function to round to the hundred thousand or five places to the left.
==ROUND() can only be used with numerical fields.==
![[Pasted image 20250115233536.png]]


## Arithmetic
We can perform basic arithmetic with symbols like plus, minus, multiply, and divide. Using parentheses with arithmetic indicates to the processor when the calculation needs to execute.
Similar to other programming languages, SQL assumes that we want to get an integer back if we divide an integer by an integer. `So be careful! When dividing`, we can add decimal places to our numbers if we want more precision.
![[Pasted image 20250115234830.png]]

What's the difference between using aggregate functions and arithmetic? The key difference is that aggregate functions, like SUM, perform their operations on the fields vertically while arithmetic adds up the records horizontally.
We will always need to use an alias when summarizing data with aggregate functions and arithmetic.
![[Pasted image 20250115235024.png]]



## NULL
 In SQL, NULL represents a missing or unknown value. Why is this useful? In the real world, our databases will likely have empty fields either because of human error or because the information is not available or is unknown. Knowing how to handle these fields is essential as they can affect any analyses we do.
 For example, we used COUNT all with an asterisk on the left. Suppose our goal is to analyze posthumous success using data from the people table. We might make the wrong assumption that because we have a field name called death_date, this information is available for everyone. Half of them are, in fact, NULL, as we can see on the right, so we would make an inaccurate judgment on what the data means.
 
One quick way to see how much of our data is missing is by using IS NULL with the WHERE clause.
Sometimes, we'll want to filter out missing values, so we only get results that are not NULL. To do this, we can use the IS NOT NULL operator.
There may be a question about the difference between using COUNT with a field name and using the same COUNT with the added WHERE clause with IS NOT NULL. `The answer is there is no difference, as both will be counting non-missing values`.


## Sorting
There are two main ways of arranging the data returned by our queries, one is ordering and the other is grouping.
### ORDER BY
In SQL, the ORDER BY keyword is used to sort results of one or more fields. When used on its own, it is written after the FROM statement. ORDER BY will sort in ascending order by default. This can mean from smallest to biggest or from A to Z.
We could also add the ASC keyword to our query to clarify that we are sorting in ascending order. The results are the same, and our code is more readable. We can use the DESC keyword to sort the results in descending order.
![[Pasted image 20250116002226.png]]

Notice that we don't have to select the field we are sorting on. However, it is a good idea to include the field we are sorting on in the SELECT statement for clarity.

ORDER BY can also be used to sort on multiple fields. It will sort by the first field specified, then sort by the next, etc. To specify multiple fields, we separate the field names with a comma. The second field we sort by can be thought of as a tie-breaker when the first field is not decisive in telling the order.
![[Pasted image 20250116151101.png]]

### GROUP BY
SQL allows us to group with the GROUP BY clause. It is commonly used with aggregate functions to provide summary statistics, particularly when only grouping a single field, certification, and selecting multiple fields, certification and title. This is because the aggregate function will reduce the non-grouped field to one record only, which will need to correspond to one group.

`SQL will return an error if we try to SELECT a field that is not in our GROUP BY clause.`

We can use GROUP BY on multiple fields similar to ORDER BY. The order in which we write the fields affects how the data is grouped.
We can combine GROUP BY with ORDER BY to group our results, make a calculation, and then order our results.
`ORDER BY is always written after GROUP BY`, and notice that we can refer back to the alias within the query. That is because of the order of execution.
![[Pasted image 20250117152529.png]]

Personally to understand this better its important to understand that Grouping things cannot be performed on a normal query, only when we do aggregate functions like counting, so.. our grouping field has to be free of modification so it can show for what it is and because of the order of execution we are first counting all the titles **and then** we can group or divide them, in this case by certifications. For me instead of grouping by its easier to understand as if we are DIVIDING IN groups. The more fields we add to group by the more subsets of smaller groups coinciding info we will get.
![[Pasted image 20250116160026.png]]


### HAVING
In SQL, we can't filter aggregate functions with WHERE clauses. Groups have their own special filtering word: HAVING.
WHERE filters individual records while HAVING filters grouped records. The reason why groups have their own keyword for filtering comes down to the order of execution.
![[Pasted image 20250117154949.png]]

By reviewing this order, we can see WHERE is executed before GROUP BY and before any aggregation occurs. This order is also why we cannot use the alias with HAVING, but we can with ORDER BY.
![[Pasted image 20250117155216.png]]


