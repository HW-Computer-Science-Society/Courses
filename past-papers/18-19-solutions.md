
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

Q2a) What is a database index?

A database index is an additional data stucture which allows fast retrieval/access of indexed fields within the database without the need o search through all the data with every lookup. The cost of this speediness is that the database index data structure requires additional writes & more storage space to maintain and is not ideal for large amounts of data.

-----

Q2b) What is an ERD and what does it show?

An ERD (Entity Relationship Diagram) are used to show the design of a database, more specifically it captures the set of entities from a database and the relationships associated with them and through this the diagram is able to show the logical structure of the database.

-----

Q2c) What is a weak entity? Include examples.

A weak entity is a type of entity which depends on the existance of a strong entity. These weak entities cannot be identified by their own atttributes and instead must rely on the key attributes of a related entity set (strong entity). An example of a weak entity could be that a room only exists if the building where the room is located exists, another example could be that a bank account can't exist without the existance of the associated bank branch.

-----

Q2d) [WIP]

-----

Q2e) Take a look at the following database relation. What are the issues with it?

| *id* | name   | dob        | deptNo | deptName
| --- | ------- | ---------- | ------ | --------
| 100 | John Pi | 01/04/1978 | 2  | Marketing
| 101 | Sarah Toms | 14/12/1985 | 2  | Marketing
| 102 | Tim Law | 01/04/1978 | 5 | HR
| 103 | Mary White | 01/04/1978 | 5 | HR

Names should probably be split into firstName & secondName to make querying the database a little bit easier. There is also duplicated data/redundancy, this can lead to errors such as when updating values like changing HR to Human Resources, this can be fixed by using a foreign key on the department numbers and a seperate table for department names.

-----

Q2f) [WIP]

-----

![question three one](images/18-19-3.1.png?raw=true "Title")

Q3ai) Projection(animalID, dateOfTreatment, amount)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&ensp;|  
Selection(A.animalID = T.animalID)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;X  
&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;|  
Selection(breed='Alsation')     Projection(animalID)  
&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;|  
Selection(amount > 50)              <ins>Treatment</ins>  
&nbsp;&nbsp;&nbsp;|         
Projection(animalID, date, amount)  
&nbsp;&nbsp;&nbsp;|  
    <ins>Animal</ins>  


-----

Q3a ii) An index is available for the breed column of the Animal table. Explain how this information is used by the optimizer.

It reduces the disk accesses required. 

-----

Q3b) Describe two advantages and two limitations of the relational model.

Advantages of the relational model:
- strong theoretical foundation (underlying algebra)
- data independence
- closed world assumption

Disadvantages of the relational model:
- limited operations (eg. no spatial or temporal operators)
- transactions lead to blocking
- hard to distribute

-----

![question three two](images/18-19-3.2.png?raw=true "Title")


Q3c i) Below is an XML Schema for a bank. Write a valid XML document containing one account that conforms with the above schema. 

```
<bank_accounts>
    <account>
        <account_number>12345678</account_number>
        <branch>
            <sort_code>123456</sort_code>
            <branch_name>BankBranch</branch_name>
        </branch>
        <given_name>Milly</given_name>
        <middle_names>Bobby</middle_names>
        <family_name>Brown</family_name>
        <balance>1234.56</balance>
    </account>
</bank_accounts>
```

-----

Q3c ii) Write an XPath expression to find the sort code for the Heriot-Watt branch. 

<code>/bank_accounts/account/branch[//branch_name="Heriot-Watt"]/sort_code</code>

![question four](images/18-19-4.png?raw=true "Title")

Q4a) What is a serialisable schedule?

Interleaving of operations from more than one transaction, in a way that it appears that one transaction took place before another. 

-----

Q4b) Consider the following sequence of operations of transactions T1 and T2. 
1. T1 reads value V
2. T2 reads value W
3. T1 deducts 1 from V
4. T2 reads value V
5. T1 writes V
6. T2 adds the value of W to V
7. T2 writes V

i) Draw a serialisability graph to show why the sequence of operations is not serialisable? Stat the reason for each edge in the graph and the property of the graph that makes it not serialisable. 

Graph: T1 ---e1---> T2 ---e2---> T1  
Edge e1 added because the read operation of T2 follows the update operation of T1 on V. 
Edge e2 added because the write operation of T1 follows the read operation of T2 on V.  
The graph is cyclic, therefore the schedule is not serialisbale according to the Serialisability Theorem. 

ii) Explain the acquisition of locks using classical 2 phase locking and the resulting problem (refer to the step numbers to state when locks are acquired). 

| step | T1 | T2 | 
| ----- | ----- | ----- |
| 1 | read V | |
| 2 | | read W |
| 3 | update V | |
| 4 | | read V |
| 5 | write V | |
| 6 | | update V |
| 7 | | write V |

1. step: T1 acquires s-lock on V. 
2. step: T2 acquires s-lock on W. 
3. step: T1 acquires x-lock on V. 
4. step: T2 blocked acquiring s-lock on V. 
5. step: T1 writes V, unlock V. 
6. step: T2 from step 4 can resume, acquire x-lock on V. 
7. step: T2 writes V, unlock V and W. 

The resulting problem is a 'dirty-read' problem. T2 will read the update value of V instead of the original (step 6). 


-----





