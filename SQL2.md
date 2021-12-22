### Joins

When we are composing a database, data will inevitably be spread across multiple tables. These tables will be related to each other through shared data. For example, we may have a User Table:

|  UserId  | Name  | Commits    |
|------- |-------|--------------|
| 01     | Jenny |  1           |
| 02     | Jose  |  2          |
| 03     | Magnolia   | 0      |
| 04     |   Rosa|  1          |

And a Commits table:

|  CommitId  | UserId  | CommitMessage    |
|------- |-------|--------------|
| 01     | 01 |  Added analytics for the product detail page       |
| 02     | 02  |  Fixed Bug in adding digital products to cart          |
| 03     | 02   | Implemented new design for home page     |
| 04     |   04|  Handled Bug in User Profile          |

So here we have two tables that have a clear relationship one to the other: Users have 0 or more commits. We can see the number of commits that a User has made without accessing the Commits table, but if we want to see the messages we need to `JOIN` the two tables. We can do that like this:

``` SQL

SELECT Users.Name, Commit.id, Commit.CommitMessage
FROM Users
JOIN Commits
ON Users.UserId = Commits.UserId
```

And our output will look like this: 

|  Name  | CommitId | CommitMessage    |
|------- |-------|--------------|
| Jenny     | 01 |  Added analytics for the product detail page          |
| Jose     | 02  |  Fixed Bug in adding digital products to cart          |
| Jose    | 03   | Implemented new design for home page      |
| Rosa    |   04|    Handled Bug in User Profile      |

We've used `JOIN` to connect this data in a helpful way. As with any other query, we can further refine this by sorting or filtering the data. 

## Types of Joins

When joining two tables, we might want to pull from records that only have data present on the two tables, or some other selection. You can think of this like Venn diagram where we may want to pull only from records that join with another, ie. all Users who Have one or more Commits. This is called an `INNER JOIN` since it looks at the part of the Venn diagram where the circles overlap. 

Let's imagine we want to find all Users with theit related Commit messages, but we still want to include Users, like Magnolia in the table above, who have made no commits. We can use a `LEFT JOIN`. ie give me all users and include their Commit information if there is any:

``` SQL
SELECT User.Name, Commit.CommitMessage
FROM Users
LEFT JOIN Commits
ON User.id = Commit.UserId;

```

|  Name  | CommitId | CommitMessage    |
|------- |-------|--------------|
| Jenny     | 01 |  Added analytics for the product detail page          |
| Jose     | 02  |  Fixed Bug in adding digital products to cart          |
| Jose    | 03   | Implemented new design for home page      |
| Magnolia    | null   | null      |
| Rosa    |   04|    Handled Bug in User Profile      |

Magnolia has been included because she is part of the 'Left' part of our join, the Users, even though there is nothing on the 'right' that corresponds to her UserId. 

Here is a handy chart to visualize different types of Joins:

![SQL_Joins](https://user-images.githubusercontent.com/692461/143931929-a3524469-c0ff-4b51-901a-a98f66c74858.jpeg)

W3's dataset has lots of related tables that you can join to get different data. Try some of the exersizes below: 

### JOIN Exercises

1) Create a query to join Customers with their respective Orders and create a table with: OrderDate, CustomerName and OrderId.

The beginning of the result will look like this: 

<img width="1049" alt="Screen Shot 2021-11-29 at 3 51 10 PM" src="https://user-images.githubusercontent.com/692461/143941277-16abfe50-c3b8-444a-8a06-7153bfac8742.png">

2) Create a query to join Order with OrderDetail, getting the sum of the quantity of total items in the order.

The beginning of the result will look like this: 

<img width="1053" alt="Screen Shot 2021-11-29 at 3 54 29 PM" src="https://user-images.githubusercontent.com/692461/143941575-e3432495-a671-4b99-997c-3bf45796d8fe.png">

## Questions about Joins

1) Given a database with Customers and Orders, where each order has a CustomerId, What kind of join would you use to find all Customers who have never placed an order? 

2) What is the difference between a Left Join and a Right Join? 


### More Exercises for W3

1. The boss has offered a prize to whichever employee packed more items in the month of August of 1996. Please write a query that shows all employees by their first and last names and how many total items (not unique items, but overall quantity) that they packed in August from most to least packed.  

![Screen Shot 2021-11-22 at 4 43 40 PM](https://user-images.githubusercontent.com/692461/142939566-383e5bf9-32a6-412a-b54e-9693907f3db1.png)


### Articles on SQL, Query Management and ORMS

[Why You Should Avoid ORMs](https://blog.logrocket.com/why-you-should-avoid-orms-with-examples-in-node-js-e0baab73fa5/). 

[ORMS are Awesome](https://chanind.github.io/2020/01/13/awesome-orms.html)

### Fun SQL Resources 

[W3 SQL](https://www.w3schools.com/sql/default.asp) - This is a real treasure as a reference. 

[LeetCode](https://leetcode.com/problemset/database/)

[SQL Murder Mystery](https://mystery.knightlab.com/) -  a great free game with lots of practice in more complex SQL queries. 

[SQL ZOO](https://sqlzoo.net/wiki/SQL_Tutorial) - lots of practice starting with very easy SQL to much more advanced. 

[SQL Police Department](https://sqlpd.com/) - This game only has a few levels for free and can feel a bit elementary, but fun none-the-less.
