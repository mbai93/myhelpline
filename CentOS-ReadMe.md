# MyHelpline

MyHelpline is a communication framework for support call centers.

[![Build Status](https://travis-ci.com/Kirembu/myhelpline.svg?branch=master)](https://travis-ci.com/Kirembu/myhelpline)
[![Coverage Status](https://coveralls.io/repos/github/Kirembu/myhelpline/badge.svg?branch=master)](https://coveralls.io/github/Kirembu/myhelpline?branch=master)
[![Documentation Status](https://readthedocs.org/projects/myhelpline/badge/?version=latest)](https://myhelpline.readthedocs.io/en/latest/?badge=latest)

## Requirements
```
 * Python 2.7
 * [Django](http://djangoproject.com/) 1.10+
 * [Asterisk](http://www.asterisk.org) 1.4+ and enabled manager
 * Redis >= 2.6.0
 * RabbitMQ
 * Nginx
 * PostgreSQL
  ```
## Technology Platform
 * Nginx
 * Python
 * Linux (Ubuntu)
 * PostgreSQL
 * Asterisk with AMI enabled.

## Installation

Install package dependencies.

```
    sudo yum install python-devel
    sudo yum install npm
    sudo yum install virtualenv
    sudo npm install -g bower
    sudo yum install gettext
    sudo yum install postgresql11-contrib
    sudo yum install python-gdal
    sudo yum install libmemcached-devel
    sudo yum install lib-devel
    sudo yum install postgis
    sudo yum install git
```




## Database setup

### In the base OS

Replace username and db name accordingly.

.. code-block:: sh

    sudo su postgres -c "psql -c \"CREATE USER helplineuser WITH PASSWORD 'helplinepasswd';\""
    sudo su postgres -c "psql -c \"CREATE DATABASE helpline OWNER helplineuser;\""
    sudo su postgres -c "psql -d helpline -c \"CREATE EXTENSION IF NOT EXISTS postgis;\""
    sudo su postgres -c "psql -d helpline -c \"CREATE EXTENSION IF NOT EXISTS postgis_topology;\""
    sudo su postgres -c "psql -d helpline -c \"ALTER USER helplineuser WITH superuser;\""



Create a virtual environment for the application.

```
    virtualenv ~/.env/
```

Activate virtual environment:

```
    source ~/.env/bin/activate
```

Install requirements:

```
    pip install -r requirements.txt
```

## Translations
 ```
  python manage.py compilemessages
 ```
Before migrations navigate to 
myhelpline/localsettings.py 
then set your database credentials as following:
```'NAME': 'name',
   'USER': ‘user’,
   'PASSWORD': 'pswd',
   'HOST': 'localhost',
   'PORT': '', 
```
 save and continue


## Migrations 
Make sure PostgreSQl is running and the cridentials for the  database are available in your "myhelpline/localsettings.py" 
```
python manage.py makemigrations
python manage.py migrate
   ```
   
## Load initial default data using fixtures

Use django fixtures we are able to load the initial default data that make setup easier.
This data includes "Hotdesks", which are a list of Soft Phone extension that can be used.
Also, we include a default service to help you get started.

```
python manage.py loaddata helpline
```


## Install components using bower
 ```
 python manage.py bower install

 ```
if running as root
```
bower install --allow-root
```
## Create User
 Run the following command and follow the prompt
  ```
  python manage.py createsuperuser
  ```
 
## Run webserver
 ```
    python manage.py runserver 0.0.0.0:8000
 ```

Go to url of the machine http://IP:8000
