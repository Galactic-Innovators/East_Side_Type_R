# AI-Powered E-Commerce App

This project is an AI-powered e-commerce application developed using the Django framework and MySQL as the database backend. It aims to provide an intuitive and efficient online shopping experience with the integration of advanced AI features.

## Prerequisites

Before you begin, ensure you have met the following requirements:
* You have installed Python 3.x.
* You have installed MySQL.If not then use this command for MacOs:
```bash
brew install mysql-client
```
Use this command for Windows:
```bash
pip install mysqlclient
```
* You have a basic understanding of Python and Django.

## Setting Up Your Development Environment

Follow these steps to set up your development environment:

### Clone the repository

```bash
git clone https://github.com/ECE651Group16/AI-Powered-E-Commerce-App.git
cd AI-Powered-E-Commerce-App
```
### Create and Activate a Virtual Environment
For Unix and MacOS:
```bash
pipenv shell
```
### Install Django in a Virtual Environment
```bash
pipenv install django
pipenv install django-debug-toolbar
pipenv shell
```
### Configure MySQL
Start the MySQL service on your machine.
Create a new MySQL database for the project:
```sql
CREATE DATABASE storefront;
```
### Update Django Settings
Navigate to the settings file at AI-Powered-E-Commerce-App/settings.py.
Configure the DATABASES setting to reflect your MySQL setup:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'root',
        'USER': 'storefront',
        'PASSWORD': 'yourpassword',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```
# Run Database Migrations
```bash
python manage.py migrate
```
# Running the Project
To run the project:
```bash
python manage.py runserver
```
The project should now be running on http://127.0.0.1:8000/.
# Create admin user
```python
python manage.py createsuperuser
```
You can log in using page http://127.0.0.1:8000/admin/

### Remember to import dummy data using Seed.sql in mysqlworkbench

# Setting up more on pipenv
## Installing Restful API, nested routers, Filtering
```bash
pipenv install djangorestframework
pipenv install drf-nested-routers
pipenv install django-filter # added into the installed apps in setting.py
pipenv install djoser
pipenv install pillow
pipenv install django-templated-mail
pipenv install djangorestframework_simplejwt

```
## Install django-cors-headers for transferring files from client to server
https://github.com/adamchainz/django-cors-headers
## Install smtp4dev for email purpose
https://github.com/rnwood/smtp4dev
Run it using docker

# Setting up for Client side
## Install NodeJS then
```bash
npm install # install dependencies
npm start
```


# For Web Performance Improvement
## Install redis (Message Brokers)& celery & flower
```bash
docker run -d -p 6379:6379 redis 
pipenv install redis 
pipenv install django-redis
pipenv install celery
pipenv install flower
```
## run celery for running bg tasks and monitor with flower
```bash
celery -A storefront worker --loglevel=info  
```
or periodic
```bash
celery -A storefront beat
```
```bash
celery -A storefront flower
```



# For Testing
## Install pytest
```bash
pipenv install --dev pytest
pipenv install --dev pytest-django
pipenv run pytest
pipenv run ptw # automated testing keep running
```

## Performance testing using locust & django-silk
```bash
pipenv install --dev locust
pipenv install --dev django-silk
pipenv install django-silk
locust -f locustfiles/browse_products.py
```

## Monitoring cache
```bash
docker exec -it CONTAINER_ID redis-cli ## select 2
...
keys *
del ...
flushall
```
# Prepare Production
```bash
python manage.py collectstatic # collecting static
pipenv install whitenoise # serving static assets
pipenv install gunicorn
gunicorn storefront.wsgi # web server gateway interface
``` 

# Deployment
using HeroKu: https://www.heroku.com/
```bash
heroku login
heroku create AI-Ecom-prod
```
### add the domain to the allowed host in prod.py
### use djecrety.ir generate the SECRET_KEY
```bash
heroku config:set SECRET_KEY = '...'
heroku config:set DJANGO_SETTINGS_MODULE=storefront.settings.prod
```
After adding SQL, HeroRedis, Mailgun in Heroku
```bash
heroku config # get MySQL:....
heroku config:set DATABASE_URL=MySQL:....
pipenv install dj-database-url
```
## Deploy:
```bash
git remote -vv
git push heroku main
heroku run bash # run in production environment
```

# Dockerize
 ```bash
docker-compose up --build
docker-compose log web
docker-compose log test
docker-compose logs -f tests
docker-compose run web bash


## Populating the database
```bash
heroku run python manage.py seed_db
heroku config:get DATABASE_URL # use it in DataGrip
```

# Contributing to AI-Powered E-Commerce App
To contribute, follow these steps:

1. Fork this repository.
2. Create a branch: git checkout -b <branch_name>.
3. Make your changes and commit them: git commit -m '<commit_message>'.
4. Push to the original branch: git push origin AI-Powered-E-Commerce-App/<branch_name>.
5. Create the pull request.
Alternatively, see the GitHub documentation on creating a pull request.

#License
This project is licensed under the MIT License - see the LICENSE file for details.
