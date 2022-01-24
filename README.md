# Python API with MySql POC

- [Python](https://www.python.org/)
- [VsCode](https://code.visualstudio.com/)

## 1. Create table

``` sql
CREATE TABLE `rest_emp` (
  `id` int(11) NOT NULL,
  `name` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `phone` varchar(16) DEFAULT NULL,
  `address` text DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

ALTER TABLE `rest_emp`
  ADD PRIMARY KEY (`id`);
  
ALTER TABLE `rest_emp`
 MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;
 ```
 ## 2. Install flask and imports
 
 ``` 
 $ pip install flask
 ```
 
 ```
 $ pip install flask-mysql 
 ```
 
 ``` python
 from flask import Flask, jsonify
 from flaskext.mysql import MySQL
 ```
 
  ## 3. Make MySql connection
  
 ``` python
  mysql = MySQL()

# MySQL configurations
app.config['MYSQL_DATABASE_USER'] = 'root'
app.config['MYSQL_DATABASE_PASSWORD'] = 'root'
app.config['MYSQL_DATABASE_DB'] = 'YOUR_OWN_DB'
app.config['MYSQL_DATABASE_HOST'] = 'localhost'

mysql.init_app(app)
  ```
 
  ## 4. Create route for request
  
  ``` python
  @app.route('/customers')
def get():
    cur = mysql.connect().cursor()
    cur.execute('''select * from rest_emp''')
    r = [dict((cur.description[i][0], value)
                for i, value in enumerate(row)) for row in cur.fetchall()]
    return jsonify({'List' : r})
  ```
 
  ## 5. Json result and link
  
  ```
  http://127.0.0.1:5000/customers
  ```
  <img src="https://i.postimg.cc/2S6JNtDc/JSON-return-python-API.png"/>
