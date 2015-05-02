---
layout: post
comments: true
title: Creating a REST Api using Flask-Restful and MongoDB
---
### About REST ###
`REST` (Representational State Transfer) is an architecture style for designing networked applications. The idea is using 
simple HTTP methods for making calls between machines rather than complex mechanisms such as `CORBA`, `RPC` or `SOAP`. 
So a RESTful system typically communicates over the Hypertext Transfer Protocol with the same HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`, etc.)

### Flask and Flask-RESTful ###
[Flask](http://flask.pocoo.org/) is a microframework for Python based on Werkzeug, Jinja2. [Flask-RESTful](https://flask-restful.readthedocs.org/en/0.3.2/) 
provides an extension to Flask for building REST APIs.

### Installing packages ###
For the api, we need to install some packages like Flask-Restful, pymongo etc. It's good practice to install packages 
and modules for a project in a virtual environment. So i am going to create a virtual environment and activate it.

```sh
$ virtualenv env
$ source env/bin/activate
```

Now the required packages can be installed using pip. (Link: [requirements.txt](https://github.com/salmanwahed/flask-restful-mongodb-api/blob/master/requirements.txt))

```sh
$ pip install -r requirements.txt
```
### API ###
Lets do the code first,

<script src="https://gist.github.com/salmanwahed/13b67bc8d77f60a495be.js"></script>

This is a basic api with only one Resource Student. First we created an instance of Flask,

```python
app = Flask(__name__)
```

after that we configured app with MongoDB. The resource Student has HTTP methods defined in it as it's own method. By 
calling different HTTP methods we can perform basic `CRUD` operations. Like `post` method for inserting/creating, `put` 
for updating, `get` for reading and `delete` for deleting a document.

In the code `post`, `put`, `delete` methods are basic.  These methods perform create, update and delete operation on the 
collection `student`. 

But in the get method, by calling different url we can perform different operations. If no parameter passed with url, 
the method will return all the documents in the collection. If a `registration` number passed with the url then, it 
will check the parameter name and will return one document. If request is made in `/api/department/<string:department>` 
url, it will check for parameter name `department` in the get method and returns all the documents for a particular department.

There are several urls for same resource so we added different [endpoints](https://flask-restful.readthedocs.org/en/0.3.2/quickstart.html#endpoints) 
for them.

### Testing ##
We will use python [requests](http://docs.python-requests.org/en/latest/) module (version > 2.4.2) for testing the api. 
But also curl and other mechanism can be used. For get request we can view the data in browsers also.

```sh
In [1]: from requests import get, post, put, delete
In [2]: get("http://127.0.0.1:5000/api")
In [3]: data = {"name": "Example Name", "registration": "123433199", "department": "cse"}
In [4]: post("http://127.0.0.1:5000/api", json=data).json()
In [5]: put("http://127.0.0.1:5000/api/123433199", json={"website": "www.example.com"}).json()
In [6]: delete("http://127.0.0.1:5000/api/123433199").json()
```
Lets take some REST.