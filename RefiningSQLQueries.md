### Getting Specific with Selectors

SQL is a powerful language with all kinds of syntax to help us tailor our queries. Let's look at a couple you may not be familiar with:

[LIKE](https://www.w3schools.com/sql/sql_like.asp) - LIKE is used to match text patterns in a particular column. It is somewhat similar to a regular expression in Javascript and other programing languages. Keep in mind that the text you are looking to match is case-insensitive.

Challenge: Write a query that returns any customers where the contactName has an a in the second and fifth position. 

[BETWEEN](https://www.w3schools.com/sql/sql_between.asp) - BETWEEN is used to search for a value, usually a number, that lies in a bounded range. The query would look something like this :

`SELECT * FROM users WHERE accountTotal BETWEEN 1000 AND 9999;`

Challenge: On the order details table, write a query that returns all orders where the quantity is between 17 and 20.  

### Grouping

When we want to see certain records collapsed into a single row, for example, when we would like to see the number of users in a certain country, we can use `GROUP BY`, passing a column. All records that have that column in common will be grouped together. 

[GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp)

Challenge: On the W3 orderDetail table, write a query that gets the number of products in each order. 

### Challenges

Select all the users that have `al` in their name.

Select orders made between this date and that. 
