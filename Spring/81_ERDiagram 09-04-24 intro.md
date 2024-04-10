ER Diagram
-

![alt text](https://i.ibb.co/g6xH0fh/image.png)

* This is the mixture of data
*  and extraction of this data is complicated 
* so we use normalization

**First Normal Form (1NF)**
Normalization in databases is the process of organizing data in a database efficiently.

* there is 3 type of normalization
* 1nf, 2nf, 3nf
* 1nf is store the data they are not in collection of values

![alt text](https://i.ibb.co/0cQCjNC/image.png)

after 1nf is done we go with 2nf form
**Second Normal Form (2NF)**
* 2nf says now every record in your table you should locate it uniquely
* firstly group the relevent column together and keep it in one table
* find the relevent between columns and group that and segregate data into multiple tables
* in every record of the table it should be an identify uniquely, it can be id, email, mobile

![alt text](https://i.ibb.co/BrvgY1q/image.png)

after 2nf is done we go with 3nf form

**Second Normal Form (2NF)**
* remove unnecessary redencency data 

![alt text](https://i.ibb.co/DG3Yd9s/image.png)

* separate all the tables based on duplicate values
* now link them together using foreign keys
* according to this we will write the hibernate code

### Mapping ###

**One to many**
```mermaid
graph LR

A((Country))
B(mike)
C(stallin)
D(adam)
A-->B
A-->C
A-->D
```

**Many to many**

![alt text](https://i.ibb.co/dP0M7rC/image.png)