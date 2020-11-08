# Python-MysqlDB-Connect

### Steps to connect MySQL database in Python using MySQL Connector Python

* Install MySQL Connector Python using pip or pip3.

```
pip install mysql-connector-python

```
Or

```
pip3 install mysql-connector-python

```

* Use the  mysql.connector.connect()  method of MySQL Connector Python with required parameters to connect MySQL.
* Use the connection object returned by a  connect()  method to create a cursor object to perform Database Operations.
* The cursor.execute() to execute SQL queries from Python.
* Close the Cursor object using a cursor.close() and MySQL database connection using connection.close() after your work completes.
* Catch Exception if any that may occur during this process.

#### Example:

```python

import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(host='localhost',
                                         database='Electronics',
                                         user='pynative',
                                         password='pynative@#29')
    if connection.is_connected():
        db_Info = connection.get_server_info()
        print("Connected to MySQL Server version ", db_Info)
        cursor = connection.cursor()
        cursor.execute("select database();")
        record = cursor.fetchone()
        print("You're connected to database: ", record)

except Error as e:
    print("Error while connecting to MySQL", e)
finally:
    if (connection.is_connected()):
        cursor.close()
        connection.close()
        print("MySQL connection is closed")
```

#### Create Table using Python:

```python

import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(host='localhost',
                                         database='Electronics',
                                         user='pynative',
                                         password='pynative@#29')

    mySql_Create_Table_Query = """CREATE TABLE Laptop ( 
                             Id int(11) NOT NULL,
                             Name varchar(250) NOT NULL,
                             Price float NOT NULL,
                             Purchase_date Date NOT NULL,
                             PRIMARY KEY (Id)) """

    cursor = connection.cursor()
    result = cursor.execute(mySql_Create_Table_Query)
    print("Laptop Table created successfully ")

except mysql.connector.Error as error:
    print("Failed to create table in MySQL: {}".format(error))
finally:
    if (connection.is_connected()):
        cursor.close()
        connection.close()
        print("MySQL connection is closed")

```

#### References:

*https://pynative.com/python-mysql-database-connection/*

*https://www.guru99.com/python-mysql-example.html*

*https://www.mysqltutorial.org/python-connecting-mysql-databases/*
