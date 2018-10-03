---
layout: post
title: RESTful API design in Python
date: 2018-09-23 13:28:49.000000000 +10:00
---
### 1.  RESTful API and application
Representational State Transfer (REST) is an architectural style that defines a set of constraints to be used for creating web services. Web services that conform to the REST architectural style, or RESTful web services, provide interoperability between computer systems on the Internet. REST-compliant web services allow the requesting systems to access and manipulate textual representations of web resources by using a uniform and predefined set of stateless operations. Other kinds of web services, such as SOAP web services, expose their own arbitrary sets of operations.
The World Bank indicators API provides 50 year of data over more than 1500 indicators for countries around the world.
### 2. Prepare
This tool is developed by Python, using data from World Bank. Data is stored in [mLab](https://mlab.com/), Database-as-a-Service for MongoDB.
#### 2.1 Python Packages
> Flask==1.0.2  
> Flask-PyMongo==2.1.0  
> flask-restplus==0.11.0  
> pymongo==3.7.1  
> requests==2.19.1

#### 2.2 Data Source
* List of indicators can be found at: http://api.w o rldbank.org/v2/indicators
* List of countries can be found at: http://api.worldbank.org/v2/countries

#### 2.3 Connect to mLab
First, import pymongo
`pip install pymongo`

Use your own mLab database parameter to build connection
```python
DB_NAME = 'database_name'
DB_HOST = 'yourhost.mlab.com'
DB_PORT = yourhost
DB_USER = 'database_user'
DB_PASS = 'database_password'

# Build connection to the database 
connection = pymongo.MongoClient(DB_HOST, DB_PORT)
db = connection[DB_NAME]
db.authenticate(DB_USER, DB_PASS)
```

return appropriate [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).
