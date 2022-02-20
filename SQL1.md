# SQL Lesson

### SQL Course Overview
  
  SQL and other query languages are used to interact with databases. As long as you work with software, you can be sure that a database - and probably more than one - is not far away. Some of you likely work with SQL on a daily basis where others might only write queries occasionally. In this class, we will review some of the basic aspects of SQL, but since you have already learned SQL basics, we will move on to some of the more advanced concepts quickly. 
  
  If you would like to review basic SQL, you can always return to the Core curriculum in [Module 4](https://github.com/joinpursuit/Pursuit-Core-Web/blob/master/full_stack_express/README.md).
  
  Throughout this two part class, we will lean heavily on [W3's Sql lessons and live database](https://www.w3schools.com/sql/default.asp). NOTE: You'll want to access W3 through Chrome. Some issues have been reported with Safari.
  
### SQL as it Relates to the Web
  
Given that we come at SQL as application developers, it is helpful to review how SQL relates to an overall application. First, SQL is a full language that we use when communicating with the database. However much, you use SQL, it's instructive to remember that there are whole career paths such as Data Science and Database Administration where SQL is a core skill. It is a large and robust language. 
  
As a web developer, we may write SQL queries, but we also have the option of including one or more pieces of software to abstract the SQL and keep us working in a more familiar language. Software that allows us to access our data in a language other than SQL are called Object Relational Mapping (ORM) programs. These exist in every web stack. With Node for example, we might use Sequelize or with Ruby, we could use Active Record. 

For a developer that would like to have more control over how a SQL query is composed, they might choose to use software generally called a query manager or composer. An example of this with Node would be pg-promise. With this, we are still using javascrip but when it comes to writing the actual query, it is esentially SQL with a bit of string interpolation. We need to understand SQL better to work effectively with this tool, but it gives a developer more control over how a query is structured. 

There is no right or wrong here, only tradeoffs in how a web application is interacting with a database. One of the main tradeoffs is whether an ORM should be engaged to make the interations with data to be as easy as possible for the developer or whether a deeper knowledge of SQL is expected with the hope that is results in a lighter application with more efficient queries. 

### Basic Review of SQL

Let's quickly review one of the bedrocks of any web application CRUD: CREATE, READ, UPDATE and DELETE. Almost everything we do in a web application is one of thesefour types of actions. Now, just as a quick reminder, let's see how CRUD maps to the HTTP methods and the SQL commands: 

|  CRUD  | HTTP  | SQL          |
|------- |-------|--------------|
| CREATE | POST  | INSERT INTO  |
| READ   | GET   | SELECT       |
| UPDATE | PUT   | UPDATE       |
| DELETE | DELETE| DELETE FROM  |

And to review SQL syntax quickly, our query is usually composed by starting with one of these key words. For example: 

`SELECT name, age, height FROM users` or 'INSERT INTO users SET score=100 WHERE age > 14'

We won't spend too much time reviewing these more simple queries, but you can practice with each of them here: 

[SELECT](https://www.w3schools.com/sql/sql_select.asp) 
[UPDATE](https://www.w3schools.com/sql/sql_update.asp)
[INSERT INTO](https://www.w3schools.com/sql/sql_insert.asp) 
[DELETE](https://www.w3schools.com/sql/sql_delete.asp)

### Articles on SQL, Query Management and ORMS

[Why You Should Avoid ORMs](https://blog.logrocket.com/why-you-should-avoid-orms-with-examples-in-node-js-e0baab73fa5/). 

[ORMS are Awesome](https://chanind.github.io/2020/01/13/awesome-orms.html)

### Fun SQL Resources 

[W3 SQL](https://www.w3schools.com/sql/default.asp) - This is a real treasure as a reference. 

[LeetCode](https://leetcode.com/problemset/database/)

[SQL Murder Mystery](https://mystery.knightlab.com/) -  a great free game with lots of practice in more complex SQL queries. 

[SQL ZOO](https://sqlzoo.net/wiki/SQL_Tutorial) - lots of practice starting with very easy SQL to much more advanced. 

[SQL Police Department](https://sqlpd.com/) - This game only has a few levels for free and can feel a bit elementary, but fun none-the-less.


