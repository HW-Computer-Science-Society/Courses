
## 17-18 solutions:



![question one](images/17-18-1.png?raw=true "Title")

Q1a) Explain what is meant by each of the following terms, and give an example of each: 

i) Database

A Database is a collection of logically related data for a particular domain. A database could, for example, be an Excel spreadsheet. 

ii) Database Management System 

A Database Management System is a software system designed for the creation and management of databases. Oracle or SQLServer would be examples of relational DBMSs (= RDBMS). MongoDB is an example of a NoSQL database program. 

iii) Database Application 

A Database Application is a program that interacts with a database during its execution. Example?? same as ii)??

----

Q1b) What are the different user roles associated with a database system? For each role state the typical types of operations they can perform on the database. 

- DBA = Database Manager: manages the database. Has detailed and extensive knowledge of the database (designs logical and physical schemas, controls security and authorisation, ...)  
- Application Developers: People who deliver the applications to the end users. Their software will query and potentially update the content of the database. Need to be aware of the logical schema/view exposed to their application.  
- End Users: People who utilise the content of the database through applications. Typically little to no knowledge of the underlying database. 

----

Q1c) Consider the following Java statements.  
<code>String username = myTextField.getText();  
String query = "SELECT * FROM Users WHERE username = '" + username + "'";</code>  

i) Describe a malicious attack that could be used to gain access to the database. 

The above examples uses string concatenation and is therefore an ad-hoc statement. SQL injection can attack ad-hoc statements easily.  
SQL injection is a malicious attack that exploits poor validation of user input. It is generally used on input fields of webforms and (due to poor validation) enables user code to be processed by the DBMS. 

ii) Describe the mechanism that would prevent the attack? (You are not required to provide the Java, but may do so)

SQL injection can be prevented by using prepared statements:  
```
String q = "SELECT * FROM Users WHERE username =?"
PreparedStatement ps = conn.prepareStatement(q); 
String value = myTextField.getText(); // get the user input
// set the first aprameter int the query to the value
ps.setString(1, value); 
```

----

![question two](images/17-18-2.png?raw=true "Title")

Q2a) Consider the following snipped of an ER diagram capturing music albums, the tracks that appear on them, and the performers (image above).  

i) Identify the mistake in the diagram and explain why it is not needed. 

The Track entity does not need a primary key because it is a weak entity. A weak entity only exists if some other entity exists; the track only exists if the album that it belongs to exists.

ii) What is a weak entity and identy one in the ER diagram? 

A weak entity depends on another entity for its existence. Details of the weak entity are only stored if the main entity exists and it won't have a candidate key. Wek entities are used to capture a composite, multi-valued attribute, eg. items in an order. 

iii) What is the primary key of a weak entity when it is translated to a table? Give an example base on the above ER diagram.  

The primary key of a weak entity is the primary key from the parent entity -> called a foreign key which references the parent entity.  
Track(<ins>albumID, trackNumber</ins>, title) 

iv) [WIP]

----

Q2b) i) Explain what an index is and the pros and cons of creating one. 

An index is an extra bit of data you add to your table. It holds a separate copy of some of the data in a different order and allows for fast retrieval/access of indexed fields without the need to search through all the data with every lookup.  
- advantage: faster retrieval/access of indexed fields, ensures uniqueness of values
- disadvantage: additional writes & storages space needed to maintain, not worth it for small relations or volatile attributes

ii) What if any indexes does MySQL create when a table is created? Use the Album table generated corresponding to the above ER diagram to give an example. 

MySQL automatically indexes the primary key of a relation. Indexing the PK also ensures uniqueness. In the above example, 
* Album.ID, 
* Artist.ID and 
* Track.albumID + Track.trackNumber (composite index)  
would be indexed automatically. 

iii) What index would you create to support queries that search for a specific album by title? 

An index on the Album.title column. 

----

Q2c) i) How is data stored in a sequential file?  

Data is stored in a sorted order (the order is determined by one filed). 

ii) Give one advantage of a sequential file.

Very efficient for retrieval, eg. especially bulk retrieval, range retrieval

iii) Give one disadvantage of a sequential file. 

Insertion requires a sort operation, sequential files are therefore bad for volatile data (every insert requires a sort)

----

![question three](images/17-18-3.png?raw=true "Title")

Q3a) i) What is a transaction?  

A transaction is a series of operations to perform a task (= logical unit of work) that takes the database from one consistent state to another. (The database is in a consistent state if it satisfies the constraints specified in the relational schema)

ii) What porperties does the Transaction Manager maintain? 

* Atomicity: all actions complete or none
* Consistency: database finishes in a consistent state
* Isolation: no interference between concurrent transactions
* Durability: changes are permanent, written data won't be lost 

iii) Outline how two phase locking enables multiple concurrent transactions. 

The two-phase locking protocol acquires locks as needed, and locks released when no longer required and no more locks will be needed. It is divided into two phases: 
* Growth phase: tranaction acquires locks as needed
* Shrink phase: transaction releases locks (& can no longer acquire locks) 

(this isn't exactly the answer to the question, idk how to answer that) 

----

Q3b) Consider the following relational schema: 
```
Country(name(PK), continent, area, population, gdp, capital)
City(name(PK), area, population)
capital is a foreign key referencing City.name
```

i) Write an SQL query to list the names of all the continents at most once. 

<code>SELECT DISTINCT continent FROM Country;</code>

ii) Write an SQL query to list the population of each continent with more than 1 billion inhabitants. 

<code>SELECT continent FROM Country GROUP BY continent HAVING SUM(population) >= 1000000000;</code>

iii) Write an SQL query to find any countries where the population of the capital city is the same as the population of the country. 

???

----

![question four one](images/17-18-4.1.png?raw=true "Title")

Q4a) i) Provide a definition fo the third normal form (3NF). 

A relation is in 3NF is it is in 2NF and all non-key attributes are mutually independent (no transitive dependencies). 

ii) What is a functional dependency and how is it used to check that a table is in 3NF? 

A functional dependency is a constraint between two sets of attributes in a relation: Let A & B be non-overlapping sets of attributes in relation R. B is functionally dependent on A if each value of A is associated with exactly one value of B. Eg. price -> tax  
Every non-key attribute in the table must be fully functionally dependent on the primary key, but it must not be a transitive functional dependency. For example, item -> price -> tax is not allowed in 3NF. 

iii) Convert the following table into 3NF. First state the functional dependencies that you use for this convesion and the provide the 3NF version. 

| courseCode | title | lecturer | email
| ---------- | ----- | -------- | -----
| F28DM-Ed | Database Systems | Alasdair Gray | a.j.g.gray@hw.ac.uk
| F28BD-Ed | Big Data Management | Alasdair Gray | a.j.g.gray@hw.ac.uk
| F28DM-Dub | Database Systems | Talal Shaikh | t.a.g.shaikh@hw.ac.uk

Functional Dependencies: 
* courseCode -> title
* lecturer -> email 

Transitive Functional Dependencies: 
* courseCode -> lecturer -> email

3NF version of the table: 

| courseCode | title | lecturerID
| ---------- | ----- | ----------
| F28DM-Ed | Database Systems | 1
| F28BD-Ed | Big Data Management | 1
| F28DM-Dub | Database Systems | 2

| lecturerID | lecturerName | email
| ---------- | -------- | -----
| 1 | Alasdair Gray | a.j.g.gray@hw.ac.uk
| 2 | Talal Shaikh | t.a.g.shaikh@hw.ac.uk

----

Q4b) i) How are missing values dealt with in an XML document? 

Missing values are ommitted (schema must allow element to be missing). 

ii) How are multiple values of the same type dealt with in an XML document, eg. storing more than one telephone number for a person? 

The element is simply repeated (schema must allow this). 

----


![question four two](images/17-18-4.2.png?raw=true "Title")

Q4b) iii) Explain why the following XML document is not well formed. (Line number are given to allow you to refer to them in your answer. They should not be considered as part of the XML document.)

The XML document is not well formed because: 
* It does not have a root element
* Line 2: The attribute F28DM-Ed must be enclosed in quotation marks. 
* Line 3: The closing tag misses the '/', it should be: 
``` <title>Database Management Systems</title>```
* Line 8: If the first letter of the starting tag is capitalised, the closing tag must be the same. 

iv) What would be the result of the following XPath query over a corrected version of the XML document in part iii)?
<code>//lecturer/text()</code>

The query would return the names of the lecturers (the text that is found between the 'lecturer'-tags). 