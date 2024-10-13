
#django #linkedin-learning #python

---
# Creating Users in Django

The admin interface is available at `localhost:8000/admin`

Django knows if the database is behind the system changes though files called migrations

Migrations explain what kind of changes a database needs to perform, such as creating new tables or establishing a new relationship

Django already has the migrations for the authentication system ready, so you need to apply them to the database through the `migrate` command

```python
python ./manage.py migrate
```

To create a superuser run:

```python
python ./manage.py createsuperuser
```

Now you can login as the superuser at `localhost:8000/admin`
# Django Admin: Easily Visualizing and Creating Data

The `localhost:8000/admin` interface is used to create, delete and manage users

# User Authentication in Two Simple Steps

Create a template for an authorized section

📁`home\templates\home\authorized.html`
```html
<html>
    <h1>You are in a restricted area</h1>
</html>
```

Create a view function for the authorized template

📁`home\views.py`
```python
from django.shortcuts import render
from django.http import HttpResponse
from datetime import datetime
from django.contrib.auth.decorators import login_required


# Create your views here.
def home (request):
    return render(request, 'home/welcome.html', {'today': datetime.today})

@login_required(login_url='/admin')
def authorized(request):
    return render(request, 'home/authorized.html', {})
```
^function-based-view

Importing `login_required` and adding `@login_required(login_url='/admin')` before the function means that a user will only be able to access the view if they are logged in

`login_url='/admin'` means that the user will be redirected to `localhost:8000/admin` if they are not logged in when they request the page