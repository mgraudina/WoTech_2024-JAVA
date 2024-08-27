## L32: Flow of data from client to db and file organisation
1. How data from client get's to the db
2. What is repository for
3. What business logic contains
4. File organisation
---------------
<img width="1000" alt="08-07-API flow" src="https://github.com/user-attachments/assets/c89c077e-21e9-4b16-bbd8-fb0464ab3fd4">

#### E.g: Change username: okklv -> okklv2

1. "Person/User" --> "API/Controller".  
"Person/User" gives input to "API/Controller".  
E.g Controller would do 2+2, send it to responsible service.  
E.g okklv2 + ID

3. "API/Controller" --> "Service/Business Logic"  
"API/Controller" sends data further to the "Service/Business logic".  
E.g Responsible service would do the actual calculations and return them.  
E.g okklv2 + userId -->  
E.g 1. Business Logic asks: Does this user exist (is this user real/exist) (repo)  
E.g 2. Validates that the username is in correct form (repo)  
E.g 3. Updates username (repo)  

4. "Service/Business Logic" --> "Data/Repository(Repo)"  
E.g Business Logic asks from data, if this user exists. 404 - not found!

5. "Data/Repository(Repo)" --> "Database"  
Database is in different server than API.  
"Data/Repository(Repo)" does QUERIES to "Database"  

------
UpdateUsername / POST method  
	1. Does this user exist

UpdateBirthYear / POST method  
	1. Does this user exist

GetProfile / GET method  
	1. Does this user exist

- To not have 3x times user check, we can ask repo to run function to check if the user exists.  
- Two different applications can use the same repo, e.g google account (gmail, youtube, GoogleDrive...etc... can log in with one user)

A database is a crucial component of the backend, but it is not the backend itself.

E.g Discord chat:  
- Message Controller  
- Message Service  
- Message Repo  
- Calls Message Table  

-->
- There is 1 database, with several tables. Like xls.
- Since repo is separate, it is more flexible, possible to test and re-use
- E.g like kiosk, you are asking for items, that are given to you, not picking up yourself

-----
* R is for data, wrangling, statistics, analytics and intelligence  
* While SQL is primarily for data storage, querying, etc. in other words CRUD OPERATIONS -->

Create  
Read  
Update  
Delete  

= CRUD

-----
TEAMWORK: CLEAN ARCHITECTURE 
-------
Discuss and find information about clean architecture -->

1. What's the importance of each layer  
2. Why is there needed some kind of structure and architecture  
3. Find other architecture types, figure out pros and cons    

https://www.educative.io/blog/clean-architecture-tutorial
