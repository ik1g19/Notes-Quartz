Create a virtual environment

```
# Windows
$ python -m venv .venv
$ .venv\Scripts\Activate.ps1
(.venv) $
```

To install django in the virtual environment

```
(.venv) $ python -m pip install django
```

To create a new Django project run

```
django-admin startproject <project_name> .
```

The period at the end `.` tells Django to setup the new project in the current directory

Django creates the structure:

```
django_project/
    __init__.py
    asgi.py
    settings.py
    urls.py
    wsgi.py
manage.py
```

- `django_hello/` is a subdirectory including five files
- `__init__.py` is an empty file that tells Python this directory should be considered a Python package
- `asgi.py` is an entry point for the new asynchronous standard ASGI
- `settings.py` contains default configurations for our project
- `urls.py` contains URL declarations for the project
- `wsgi.py` is an entry point for WSGI web servers, the older synchronous standard. Django supports _both_ ASGI and WSGI
- `manage.py` is a command line utility to help us interact with the Dango project.

