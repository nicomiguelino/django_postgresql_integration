# Integrating PostgreSQL with Django

This repository contains a Django project that uses PostgreSQL as its database.


## Setup

***Note:*** PostgreSQL must be installed first.

### Install psycopg2

```bash
pipenv install psycopg2
```

### Open psql and enter the following commands

***Note:*** We've assumed that you've logged in using your PostgreSQL superuser account `postgres`.

```sql
CREATE USER myuser WITH ENCRYPTED PASSWORD 'mypass';

ALTER ROLE myuser SET client_encoding TO 'utf8';
ALTER ROLE myuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE myuser SET timezone TO 'UTC';

GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;
```

Enter `\q` to quit psql.

### Modify `settings.py`

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mydb',
        'USER': 'myuser',
        'PASSWORD': 'mypass',
        'HOST': 'localhost',
        'PORT': ''
    }
}
```

### Create a superuser and migrate to database

```bash
python manage.py createsuperuser # You will be prompted to enter a password.
python manage.py migrate # This will populate your recently-created database with tables.
```

You could check pgAdmin for verification.

![screenshot_01](/images/screenshot_01.png)


## References

- [PostgreSQL Tutorial - Install PostgreSQL](https://www.postgresqltutorial.com/install-postgresql/)
- [Django Central - Using PostgreSQL with Django](https://djangocentral.com/using-postgresql-with-django/)
