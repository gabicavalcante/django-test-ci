# A Semaphore demo CI/CD pipeline using Python Django

Example Python Django application and CI/CD pipeline for integrating it with GitHub CI/CD.
This application demonstrates CRUD operations using class based views in Django. It also includes UI for all CRUD views.
And it's based on this tutorial: https://semaphoreci.com/blog/python-continuous-integration-continuous-delivery.

# Local project setup

1. Use virtualenv for setting up this project

2. Install pip requirements
   ```
   pip install -r requirements.txt
   ```
3. Create new psql database
   ```
   postgres=# create database pydjango;
   ```
4. Setup your database credentials and `SITE_URL` in settings.py file available inside ### core folder

5. Once you have setup your database, Open command prompt pointing to the Root of the project directory and run following command to create application default database

   ```
   (virtualenv / conda environment) > python manage.py migrate

   (virtualenv / conda environment) > python manage.py createsuperuser
   ```

6. Once all of the above command run sucessfully, We are ready to go. Start server by executing command
   ```
   (virtualenv / conda environment) > python manage.py runserver
   ```
   and visit the web browser with 'http://127.0.0.1:8000'

## Environment variables

The following environment variables can be set to override defaults:

- `SECRET_KEY`: Django [secret key](https://docs.djangoproject.com/en/2.2/ref/settings/#secret-key).
- `DB_ENGINE`: Django database [backend](https://docs.djangoproject.com/en/2.2/ref/databases/).
- `DB_NAME`: database name.
- `DB_HOST`: database hostname.
- `DB_PORT`: database port.
- `DB_USER`: database user.
- `DB_PASSWORD`: database password.

# CI/CD GIthub

The example pipeline contains 3 blocks:

- Install Dependencies
  - Installs pip requirements
- Run Code Analysis
  - Run code analysis / code linting with Pylint
- Run Unit Tests
  - Runs Unit Tests with pytest module for views and models file

# Test with PyTest

To tell pytest witch Django settings that should be used for tests runs, we need to setup a pytest configuration file, called `pytest.ini` in our project root directory. The file contains:

```
[pytest]
DJANGO_SETTINGS_MODULE=core.test_settings
addopts = --nomigrations --cov=. --cov-report=html
```

To run the tests, we can invoke directly `pytest` command instead of `manage.py test`.
The pytest-django is designed to run with the `pytest` command, but in case of you want to use `manage.py test` with pytest-django, you can create [a simple test runner](https://pytest-django.readthedocs.io/en/latest/faq.html#how-can-i-use-manage-py-test-with-pytest-django).
