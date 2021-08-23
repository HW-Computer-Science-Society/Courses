These are in randomised order

**F28DM Sample Exam**

---

Question 1:

For the following snippet of XML Schema, give one valid value for accountType.
![image](https://user-images.githubusercontent.com/65869535/117819710-b9942e00-b261-11eb-86ba-5c67d78d54a0.png)

Answer: Current (Alternatively: Savings or Student)

---

Question 2:

What does the S stand for in RDBMS? 

Answer: system

---

Question 3:

Explain how strict two phase locking prevents the 'dirty read' problem.

Answer: Strict 2PL ensures that data/information written by an uncommitted transaction has an exclusive lock, 
this prevents other transactions from ‘dirty’ reading this data and this lock is kept until the transaction is committed. 

---

Question 4: 

Hierarchical databases have existed since the invention of XML 

Answer: False

---

Question 5:

State the line numbers that contain validation errors
![image](https://user-images.githubusercontent.com/65869535/117820785-c82f1500-b262-11eb-9547-9b266b6806c9.png)

Answer: 3, 5

---

Question 6:

Consider the following XML data. Write an XPath query to return the titles of the movies as a string.
![image](https://user-images.githubusercontent.com/65869535/117820938-f6acf000-b262-11eb-8846-3bdfb43be7d4.png)

Answer: /movies/movie/title/text()

---

Question 7:

Conservative two phase locking (2PL) means:

Answer: All locks are acquired at the start of the transaction

---

Question 8:

Put these design steps into the correct chronological order from project inception.

Answer: Problem Definition, Data Requirements, Conceptual Data Model, Logical Schema, Physical Schema

---

Question 9:

Which term represents the fact that a transaction can't be divided into smaller parts?
		
- Isolation
 		
- Atomicity
 		
- Durability
 		
- Consistent

Answer: Atomicity

---

Question 10:

Let V = 5, W = 7, and Z = 15 . What value does each variable have at the end of this schedule?
![image](https://user-images.githubusercontent.com/65869535/117822011-0d077b80-b264-11eb-81f0-13ed278659d2.png)

Answer: 5, 7, 30

---

Question 11:

How are missing values represented in the relational model?
	
- Not supported
 		
- Tags are omitted
 		
- NULL value
 		
- No value between two commas

Answer: NULL value

--- 

Question 12:

Tedd Codd suggested guidelines for structuring a relational database to reduce data redundancy. What's it called?
		
- Entity Relationship Diagram
 		
- SQL
	
- Normal Forms
 		
- Recursive Relationship

Answer: Normal Forms

---

Question 13:

Take a look at the following entity specialisation.
For the relational schema generated pick the corresponding membership case (tick all that apply).

![image](https://user-images.githubusercontent.com/65869535/117822373-6a9bc800-b264-11eb-9a31-a9be547a4ca4.png)

Person (ssn, firstName, lastName, dateOfBirth, gender, employeeFlag, clientFlag, salaryGrade)
		
- mandatory
		
- optional
		
- and
		
- or

Answer: mandatory, and

---

Question 14:

SQL consists of DDL, DML, TCL, DCL.

Fill in the missing words below.

- DDL - data ...... language
- DML - data ...... language
- TCL - ...... ......  language
- DCL - data ...... language 

Answer:
- DDL - data definition language 
- DML - data manipulation language 
- TCL - transaction control language 
- DCL - data control language

---

Question 15:

Assume that the Animal table is many times larger than the Treatment table, and there is an index available on the breed column of the Animal table. 
Which of the  optimization steps should be applied to the following query plan?

![image](https://user-images.githubusercontent.com/65869535/117823287-38d73100-b265-11eb-999c-7799280bd6c0.png)

Answer: Push selection; Index lookup instead of table scan; Introduce projection.  

Explanation: In this case, the Animal table is a lot larger than the Treatment table so we would keep it on the left of the join operation. This means that we cannot use the nested loops join, as the index look up needs to be the inner relation. Therefore, we would push the selection down and then introduce an index look up on the Animal table rather than a full table scan. Finally, to make things smaller we would introduce projections.
