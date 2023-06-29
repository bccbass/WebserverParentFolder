
# **PesonnelAPI**
## README.md
</br>

![Record Store by Mick Haupt](./docs/mick-haupt-CbNBjnXXhNg-unsplash.jpg)
##### *Photo by Mick Haupt (unsplash)*  

</br>

### **Contents:**
1. [Quickstart](#Quickstart)
1. [Project Purpose](#Project-Purpose-(R1,-R2))
1. [Why PostgreSQL (R3)](#Why-PostgreSQL-(R3))
1. [ORM: Benefits and functionality (R4)](#ORM:-Benefits-and-functionality-(R4))
1. [Endpoints (R5)](#Endpoints-(R5))
1. [ERD (R6)](#ERD-(R6))
1. [Third Party Services (R7)](#Third-Party-Services-(R7))
1. [Project Models (R8)](Project-Models-(R8))
1. [Database Relations (R9)](Database-Relations-(R9))
1. [Project Management (R8)](Project-Management-(R10))

### ***Links:***

- #### [Github Repository](https://github.com/bccbass/PersonnelAPI)
- #### [Trello Project Management](https://trello.com/invite/b/VWm2omOk/ATTI837dd0d277594dd006695995cdfdac5787BC1FFE/personnel-api)
- #### [API Endpoints](./API-Endpoints.md)

</br>


## ***Quickstart***  

1. Open a new terminal window, run PSQL and create a new PostgreSQL database entitled `personnel`:
    ```psql
    ~psql
    CREATE DATABASE personnel;
    ```
2. Connect to the new database:
    ```psql
    \c personnel
    ```
3. Create a New User, set a Password and grant all privileges:
    ```psql
    CREATE USER <user> WITH PASSWORD <password>;

    GRANT ALL PRIVILEGES ON <database_name> TO <user>;
    ```
4. In the main project directory create a ```.env``` file using ```.env.sample```  as a template. 
    - The Database URI should be formatted as ```Database+adapter://<user>:<password>@<host name>:<port>/<database>```
        
        eg: ```
        DATABASE_URI='postgresql+psycopg2://<YOUR_USER_NAME>:<YOUR_USER_PASSWORD>@localhost:5432/personnel'```
    - The JWT Secret sould be something secure. 
        - Hint:
        generate secret code in the terminal:
        ```
            # $ python3 -c 'import secrets; print(secrets.token_hex())'
        ```
5. You should now be able to run the bash script from the terminal to create a .venv folder, install requirements, set up the database tables and seed them with sample date: 
    ```
    $ bash create_and_seed.sh
    ```

6. Now that the database and project environments are set up, to run the app from the terminal activate the virtual environment:
    ```
    $ source .venv/bin/activate
    ```
    and run the program:
    ```
    $ flask run
    ```
</br>
</br>
### **Project Purpose (R1, R2)**

There is currently no centralized database cataloging all the musicians that performed and contributed to recorded albums. While the information can be searched for on the internet it is usually found in disparate places with varying degrees of accuracy. Because the music industry has largely been driven by profit motive with little incentive to document the artistic product being created a great deal of data is either missing or hard to access. It is only with the privilege of hindsight that the cultaral importance of the contributions of the many side musicians has come into light, as can be seen with many books and documentaries(Muscle Shoals(2013), The Wrecking Crew(2014)) illuminating the seledom visited world of supporting session musicians. The App creates a platform to document musical contributions and query the information in many ways, such as discovering all session musicians that peformed on your favorite song, or listing all of the tracks a given musician played on. The Personnel API seeks to address to the problem of a historical lack of addredidation of musical contributions, important to scholarly and cultural research as well as for its role in providing financial compensation for contributing artists and their heirs. The Personnel API seeks to create a rich ecosystem for music fans and scholarly researchers alike to find information about our musical cultural heritage.


</br>  
</br>  

### Why PostgreSQL (R3)
I chose PostgreSQL for the Personnel API project because it is an extremely robust relational database management system that excels at both small and production level scale. It has over thirty-five years of support and development by an active community with an extensive set of open source tools, libraries and frameworks. PostgreSQL supportas a huge amount of datatypes with approprate validation and constraints for each. PostgerSQL is adept at promoting data integrity and durability, implementing ACID (Atomicity, Consistency, Isolation, Durability) transactions, write-ahead logging (WAL) and point-in-time recovery. PostgreSQL query language is extremely powerful with near limitless parameters for retrieving records. Because PostgreSQL is primarily designed for SQL databases it promotes well defined relational data structures that are strongly typed, with many optional constraints and validations ensuring data integrity and robustness. The Personnel API database leverages a relational model with join tables and multiple relational associations making PostgreSQL a clear forerunner for creating and managing these associations, facilitating querying and manipulating data with complex interacting relationships. The web-like nature of artistic careers and associations that can span decades with abundant overlapping relationships pose a huge challenge to model logically and economically, but PostgreSQL excels at managing a dataset that has a tendency towards duplicate data. After normalization it promotes a database with no redundant data, promoting data integrity and conservative usage of resources with regard to both storage and querying and manipulation of data.

Some drawbacks of PostgreSQL compared to other Database Management Systems are that it is marginally more difficult to set up, and marginally slower compared to some lighter weight frameworks such as MySQL. However with ample documentation and functionality with regard to data integrity, validation and constraints features this seemed like a reasonable tradeoff. Additionally, compared to a NoSQL DBMS PostgreSQL requires much more planning and modelling at the outset of the project, and poses more challenges to restructure the database should the scope or needs of the project change throughout production. However this is less an issue with PostgreSQL itself and more in the scope of an SQL vs NoSQL database debate.


</br>  
</br>  

### ORM: Benefits and functionality (R4)

**Functionality:**
An Object Relational Mapper (ORM) acts as a layer between a databse and higher level programming languages and framewords such as Python and Flask. Its main functinality is to provide mapping between a chosen database and an object oriented prgramming language, allowing the user to interact with a database converting native classes to tables and objects to database records. The user can implement the full range of CRUD operations within the database in a familiar language, versus incorporating SQL syntax and commands within their code; the ORM then translates these directives into SQL in order to interact with the database more seamlessly. Additionally, querying can accomplished using more familiar syntax, excluding the need to incorporate SQL queries within the codebase. ORMs also provide functionality to construct and manage relationships and associations, automatically connecting related entities and performing integrity checks such as those relating to foreign key constraints without having to manually ensure integrity is enforced. ORMs are generally database agnostic, meaning they can be connected to many different DBMS's, granting a great deal of flexiblity and universality to the database an app interacts with, without having to functionally alter it. Most ORM's( either nativley or through extensions) provide functionality to convert datatypes, including between native datatypes, database datatypes and JSON. They can also offer addtional schema construction as well as data sanitisaztion and validation. Lastly, the ORM provides functionality for creating and constructing transactions by using a session object, giving the user the ability to interact with the database in more complicated ways before commiting any changes to the database by commiting the constructed session object.  

**Benefits:** ORMs are essential to interacting with databases on the application level. They allow the developer to forego including SQL or other targeted database syntax into their code. Using higher level language to interact with a database saves time in development and creates a more streamlined codebase. Constructing a databases tables, with defined constraints can be accomplished using an Object Oriented Approach, allowing for easy DDL that can be updated or changed at the application level, foregoing the need to directly interact with the database to define tables. Querying can also be accomplished with language more familiar to the high level programming language, foregoing the need to learn, understand and implement the more specified language of database queries, such as those found in SQL. ORMs provide a great deal of functionality with conversion of datatypes, allowing for datatypes to be converted between queries and commits with out ,much consideration necessary by the developer, eliminating the need to manually convert datatypes constantly. Relationships and associations can be accomplished with very little effort, providing huge payoffs with functionality, eliminating the need for continally defining or querying related records. These nested records can further be configured by implementing Schemas (either natively or through extensions such as Marshmallow). Using schemas can also be extremely powerful with regard to validating and sanitizing user information before commiting to the database, further enabling data integrity.


</br>  
</br>  

### **Endpoints (R5)**  

***[See API-Endpoints.md](./API-Endpoints.md)***



</br>  
</br>  

### **ERD (R6)**
![Personnel ERD](./docs/Personnel_ERD.jpg)


</br>  
</br>  

### **Third Party Services (R7)**

     
- [**Flask-Bcrypt**](https://flask-bcrypt.readthedocs.io/en/1.0.1/ )  
    Implemented for Password hashing. Bcrypt is designed to be 'de-optimized', making it much more difficult to crack with the prevalence of powerful modern hardware. 



- [**Flask**](https://flask.palletsprojects.com/en/2.3.x/)  
    Flask is a lightweight Python web framework and is the context our app is created in. It is implemented primarily to handle HTTP request/response cycles, routing, accepting user data in teh form of JSON to be handled and stored in the database, or serving JSON responses from https requests.   

      


- [**Flask-JWT-Extended**](https://flask-jwt-extended.readthedocs.io/en/stable/) 
    JWT was implemented to create and manage JWT tokens, aiding functionality for authentication. Its primary uses are for token managemnt, creating bearer tokens and authenticating bearer tokens. 


- [**Flask-SQLAlchemy**](https://flask-sqlalchemy.palletsprojects.com/en/3.0.x/)  
    Implemented as an Object Relational Mapper (ORM) to facilitate interacting with a PostgreSQL database. 
    

- [**Flask-Marshmallow**](https://flask-marshmallow.readthedocs.io/en/latest/)  
    Flask-Marshmallow was used to serialize/deserialize objects between python and the database, as well as converting python objects to JSON for HTTP responses. It is also used heavily in constructing model schemas and user input validation/sanitization.
    

- [**PostgreSQL**](https://www.postgresql.org)  
    The relational database used for the Personnel App is PostgreSQL.  
    

- [**Pyscopg2-binary**](https://pypi.org/project/psycopg2/)   
    SQLAlchemy is database agnostic so an adaptor must be implemented as a utility to connect it to the PostgreSQL database.  
    

- [**Python-dotenv**](https://pypi.org/project/python-dotenv/)   
    Python-dotenv reads key-value pairs from the .env file, allowing the app to access this data through the environ module. This helps to encapsulate sensitive information, protecting the integrity of the app from malicious actors.  
    

</br>
</br>

### **Project Models (R8)**

</br>
</br>




### **Database Relations (R9)**

</br>
</br>

### **Project Management (R10)**

</br>
</br>


