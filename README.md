
# **PesonnelAPI**
## README.md
</br>

![Record Store by Mick Haupt](./docs/mick-haupt-CbNBjnXXhNg-unsplash.jpg)
##### *Photo by Mick Haupt (unsplash)*  

</br>

### **Contents:**
1. [Project Purpose](#Project-Purpose-(R1,-R2))
1. [Why PostgreSQL (R3)](#Why-PostgreSQL-(R3))
1. [Endpoints (R5)](#Endpoints-(R5))

### ***Links:***

- #### [Github Repository](https://github.com/bccbass/PersonnelAPI)
- #### [Trello Project Management](https://trello.com/invite/b/VWm2omOk/ATTI837dd0d277594dd006695995cdfdac5787BC1FFE/personnel-api)
- #### [API Endpoints](./API-Endpoints.md)

</br>

### **Project Purpose (R1, R2)**

There is currently no centralized database cataloging all the musicians that performed and contributed to recorded albums. While the information can be searched for on the internet it is usually found in disparate places with varying degrees of accuracy. Because the music industry has largely been driven by profit motive with little incentive to document the artistic product being created a great deal of data is either missing or hard to access. It is only with the privilege of hindsight that the cultaral importance of the contributions of the many side musicians has come into light, as can be seen with many books and documentaries(Muscle Shoals(2013), The Wrecking Crew(2014)) illuminating the seledom visited world of supporting session musicians. The App creates a platform to document musical contributions and query the information in many ways, such as discovering all session musicians that peformed on your favorite song, or listing all of the tracks a given musician played on. The Personnel API seeks to address to the problem of a historical lack of addredidation of musical contributions, important to scholarly and cultural research as well as for its role in providing financial compensation for contributing artists and their heirs. The Personnel API seeks to create a rich ecosystem for music fans and scholarly researchers alike to find information about our musical cultural heritage.


</br>  
</br>  

### Why PostgreSQL (R3)
PostgreSQL is an extremely popular and relational database management system that excels at production level scale. It is open sourced and has over thirty-five years of support and development by an active community. Because of this PostgresQL enjoys frequent updates, upgrades and bug fixes. The open-source community has also developed extensive tools, libraries and frameworks which enable integration into many languages and project environments. Although PostgreSQL does support NoSQL databases it is primarily aimed towards managing SQL databases - a database structure that was created in the early 1970's. This history results in ample documentation and a set of tried and tested best practices for creating robust and efficient databases. PostgreSQL supports many data types including geolocation, geospatial as well as user defined data types and functions. PostgerSQL is adept at promoting data integrity and durability, implementing ACID (Atomicity, Consistency, Isolation, Durability) transactions, write-ahead logging (WAL) and point-in-time recovery. DDL, DML and DQL in PostgreSQL are extremely straightforward using directives that more closely resemble plain english than code. PostgreSQL query language is extremely powerful with near limitless parameters for retrieving records. Because PostgreSQL is primarily designed for SQL databases it promotes well defined relational data structures that are strongly typed, with many optional constraints and validations ensuring data integrity and robustness.



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
    Flask is a lightweight Python web framework implemented primarily to handle HTTP routing.  

      


- [**Flask-JWT-Extended**](https://flask-jwt-extended.readthedocs.io/en/stable/) 
    JWT was implemented to create and manage JWT tokens, aiding functionality for authentication.


- [**Flask-SQLAlchemy**](https://flask-sqlalchemy.palletsprojects.com/en/3.0.x/)  
    Implemented as an Object Relational Mapper (ORM) to facilitate interacting with a PostgreSQL database. 
    

- [**Flask-Marshmallow**](https://flask-marshmallow.readthedocs.io/en/latest/)  
    Flask-Marshmallow was used to serialize/deserialize objects between python and the database, as well as converting python objects to JSON for HTTP responses. It is also used heavily for validation.
    

- [**PostgreSQL**](https://www.postgresql.org)  
    The relational database used for the Personnel App is PostgreSQL.  
    

- [**Pyscopg2-binary**](https://pypi.org/project/psycopg2/)   
    SQLAlchemy is database agnostic so an adaptor must be implemented as a utility to connect it to the PostgreSQL database.  
    

- [**Python-dotenv**](https://pypi.org/project/python-dotenv/)   
    Python-dotenv reads key-value pairs from the .env file, allowing the app to encapsulate sensitive information thereby protecting the integrity of the app from malicious actors.  
    

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


## ***Quickstart***  

1. Create a new PostgreSQL database entitled 'personnel':
    ```psql
    CREATE DATABASE personnel
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
4. Create a ```.env``` file in the main project directory, using ```.env.sample```  as a template. 
    - The Database URI should be formatted as ```Database+adapter://<user>:<password>@<host name>:<port>/<database>```
        
        eg: ```
        DATABASE_URI='postgresql+psycopg2://<YOUR_USER_NAME>:<YOUR_USER_PASSWORD>@localhost:5432/personnel'
        ```
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

6. Now that the database and project environments are set up, to run the app from the terminal:
    ```
    $ source .venv/bin/activate
    ```
    and run the program:
    ```
    $ flask run
    ```
    