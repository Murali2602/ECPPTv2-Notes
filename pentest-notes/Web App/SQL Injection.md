# SQL Injection

## Source - [PortSwigger Academy](https://portswigger.net/web-security/sql-injection)
#### What is SQL Injection - 
SQL injection is a vulnerability where an attacker can interfere with queries made to a database system and eventually modify/delete stuff inside the database. They will be able to access other users data or any other data that the application is able to access.

#### Some common SQL injection examples - 
- ***Retrieving the hidden data*** - `where you can modify an SQL query to return additional results.`
- ***Subverting hidden logic*** - `where you can change a query to interfere with the application's logic.`
- ***UNION attacks*** - `where you can retrieve data from different database tables.`
- ***Examining the database*** - `where you can extract information about the version and structure of the database.`
- ***Blind SQL Injection*** - `where the results of a query you control are not returned in the application's responses.`

1. ***Retrieving the hidden data - ***

	- Suppose there is a website that is vulnerable to SQL Injection and the user clicks on `Users`, the browser will request the URL - `http://vulnerable-site.com/accounts?category=Users`
	- This causes the application to make an SQL query to retrieve the Users from the database - `SELECT * FROM accounts WHERE category = 'Users' and Type = 1`
	- Here there is a restriction being used i.e 'Type = 1' is making sure that only 'Users' from 'Public' are being displayed. For private, presumably 'Private = 0'
	-  The application doesn't implement any defenses against SQL injection attacks, so an attacker can construct an attack like: `http://vulnerable-site.com/accounts?category=Users'--`
	-  This results in the SQL query: `SELECT * FROM accounts WHERE category = 'Users'--' AND released = 1`
	> **Note** - ***The key thing here is that the double-dash sequence `--` is a comment indicator in SQL, and means that the rest of the query is interpreted as a comment. This effectively removes the remainder of the query, so it no longer includes `AND released = 1`. This means that all products are displayed, including unreleased products.***
	-  Going further, an attacker can cause the application to display all the products in any category, including categories that they don't know about - `http://vulnerable-site.com/accounts?category=Users'+OR+1=1--`
	-   This results in the SQL query: `SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1`
		***The modified query will return all items where either the category is Gifts, or 1 is equal to 1. Since 1=1 is always true, the query will return all items.*** 

2. ***Subverting application logic - ***
	-  Consider an application that lets users log in with a username and password. If a user submits the username `murali` and the password `kajal`, the application checks the credentials by performing the following SQL query: `SELECT * FROM users WHERE username = 'murali' AND password = 'kajal'`
	- If the query returns the details of a user, then the login is successful. Otherwise, it is rejected.

	- Here, an attacker can log in as any user without a password simply by using the SQL comment sequence `--` to remove the password check from the `WHERE` clause of the query. For example, submitting the username `administrator'--` and a blank password results in the following query: -`SELECT * FROM users WHERE username = 'administrator'--' AND password = ''`
	
	-  This query returns the user whose username is `administrator` and successfully logs the attacker in as that user
