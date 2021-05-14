
## 18-19 paper:



![question one](images/18-19-1.png?raw=true "Title")

Q1ai) Name 4 types of integrity constraint supported in an RDBMS, and give an example of each.

**Domain constraints**: ensures the validity of entries within a column <br/> 

| ID | NAME | AGE |
| -- | --- | --|
| 1 | Cade | 12 |
| 3 | Xander | 83 |
| 2 | Frank | Yes |

^ Violates contraint as 'Yes' is not an integer value which AGE requires.

**Entity constraints**: primary key for a given row needs to be unique & no component of a primary key can be NULL <br/>

| ID | NAME | AGE |
| -- | --- | -- |
| NULL | Cade | 12 |
| 2 | Xander | 83 |
| 2 | Frank | 34 |

^ Violates contraint as a NULL value is in one of the primary key fields, also the primary key value 2 is repeated so it is not unique

**Referential constraints**: foreign key value must either reference a primary key value of the referenced table or be set to NULL <br/>

Person Table:
| ID | NAME | ORDER |
| -- | -- | -- |
| 1 | Cade | 1 |
| 3 | Xander | 2 |
| 2 | Frank | 5 |
| 4 | Andrew | 3 |
| 5 | Kurt | NULL |

Menu Table:
| ORDERID | ITEM |
| --- | -----
| 1 | Lemonade |
| 2 | Rum |
| 3 | Orange Juice |

^ Violates contraint Frank orders an item with an ID of 5 which doesn't exist within the menu

**Custom constraints**: constraints which aren't covered by the others such as not allowing a value to be NULL <br/>

```
CREATE TABLE Person (
    ID int NOT NULL,
    NAME varChar(20) NOT NULL,
    ORDER int
);
```

^ Puts a constraint on the ID & NAME attributes which enforces their participation by not allowing them to have a NULL value

-----

Q1aii) Explain what CRUD stands for and give the appropriate related SQL operation in each case.

C: Create [INSERT]<br/> 
R: Read [SELECT]<br/> 
U: Update [UPDATE]<br/> 
D: Delete [DELETE]<br/> 

-----

Q1b) What is SQL injection and which steps should be taken to prevent it from happening?

SQL injection is a malicious attack usually against websites and input fields used within them. It's done by exploiting poor input validation which allows dangerous user inputted code to be parsed & processed by the DBMS used by the website. There are many ways to prevent SQL injection, examples include:

- controlling user input by using selection boxes/drop down menus where applicable
- input validation which replaces potentially dangerous inputs with different/altered inputs
- using prepared statements to limit the SQL that can be injected and storing inputted SQL commands as strings
- avoiding the use of string concatenation
- limiting the provided privileges for the database

-----

Q1c) Give the results (including column names) from each of the following SQL statements based on the tables T1 and T2.

<br/>

**T1**
| id | value |
| - | - 
| 1 | a
| 2 | b
| 3 | c

<br/>

**T2**
| id | value |
| - | - 
| 2 | x
| 3 | y
| 4 | z

-----

Q1ci) SELECT t1.value AS v1,t2.value AS v2 <br/> FROM T1 JOIN T2 ON t1.id=t2.id;

b|x<br/>
c|y

-----

Q1cii) SELECT t1.value as v1, t2.value as v2 <br/> FROM T2 LEFT JOIN T1 ON t2.id=t1.id;

b|x<br/>
c|y<br/>
|z

-----

Q1ciii) SELECT t1.id as id1 ,t2.id as id2 <br/> FROM T1, T2;

1|2<br/>
1|3<br/>
1|4<br/>
2|2<br/>
2|3<br/>
2|4<br/>
3|2<br/>
3|3<br/>
3|4<br/>

-----

Q1civ) SELECT t1.value as v1, t2.value as v2 <br/> FROM T1 LEFT JOIN T2 on t1.id=t2.id <br/> UNION <br/>
SELECT t1.value as v1, t2.value as v2 <br/> FROM T2 LEFT JOIN T1 on t2.id=t1.id;

|z<br/>
a|<br/>
b|x<br/>
c|y<br/>

-----

Q1cv) SELECT * FROM T1 <br/> WHERE t1.id NOT IN (SELECT id from T2);

1|a

-----

![question two](images/18-19-2.png?raw=true "Title")

![question three one](images/18-19-3.1.png?raw=true "Title")

![question three two](images/18-19-3.2.png?raw=true "Title")

![question four](images/18-19-4.png?raw=true "Title")



