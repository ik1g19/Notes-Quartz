
#django #linkedin-learning #python
# Used for this Project

- Python 3.8 venv
- Django 3.2

# Creating a new Django Project

Create a new environment

```python
python -m venv venv
```

And install Django

```python
pip install Django
```

Run

```python
django-admin startproject smartnotes .
```

to create a project called 'smartnotes' in the current directory

This create a `manage.py` - the entry point of the project, and a directory called smartnotes

Inside the smartnotes directory, are files related to the configuration of the project
- `urls.py` is used to configure the urls of the project

Start the server with

```python
python manage.py runserver
```

The default port is 8000

# Minimum Working Page

Use `django-admin` again to create a new app called home

```python
django-admin startapp home
```

A new directory called 'home' is created, this is the new app

Every time we create a new app we need to add it to the settings file so it knows that the folder is a part of the project we're running

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    #apps
    'home',
]
```

## Creating the First View

📁`home/views.py`
```python
from django.shortcuts import render
from django.http import HttpResponse
from datetime import datetime

  

# Create your views here.
def home (request):
    return HttpResponse('Hello World')
```

📁``smartnotes/urls.py``
```python
from django.contrib import admin
from django.urls import path, include

from home import views


urlpatterns = [
    path('admin/', admin.site.urls),
    path('home', views.home)
]
```

Going to `localhost:8000/home` will render the view

When a person goes to the home endpoint, they are making a request to that path

Django will go to the `urls.py` file to see if it's ready to receive a request at this path

Since it is, it will go to the views file, arriving at the function we defined

Django use a Model View Template pattern framework

# Creating your First Django Template

Create `home/templates`, inside this create another folder called `home` for our app template

This allows us to quickly identify where a template is located, even if we don't know which app we are on

In this folder we create `welcome.html`

`home/templates/home/welcome.html`
```html
<html>
    <header><title>SmartNotes</title></header>
    <body><h1>Welcome</h1></body>
    <p>Today is {{today}}</p>
</html>
```

Now we go back to the views file and use the render function, we pass it the original request, the name of the template and any information to be passed down to the template

Although we wrote a HTML page, Django is actually using a template framework to create the final HTML page that we see in the browser (Django Template Language or **DTL**) ^e6a487

📁`home/views.py`
```python
from django.shortcuts import render
from django.http import HttpResponse
from datetime import datetime

# Create your views here.
def home (request):
    return render(request, 'home/welcome.html', {'today': datetime.today})
```

DTL allows creating dynamic and sophisticated HTML pages with very little effort

# Django Apps and the Concept of Modularization

Each Django app should be self contained

The ideal app is where you can delete the app folder and the Django project will continue to work

When creating the first endpoint, we imported the views file from home into the urls file in the smartnotes folder

This creates a dependency that wouldn't allow us to delete the home app

![[Images/Pasted image 20240828145242.png]]

So we create another url file in the home app

📁`home/urls.py`
```python
from django.urls import path

from . import views

urlpatterns = [
    path('home', views.home)
]
```

In the smartnotes url file we can now remove the home dependencies

📁`smartnotes/urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('home.urls'))
]
```

We now use the include function to pass the file as a string

Now the home app folder could be deleted and the Django project would still work as it is no longer being imported on the smartnotes file