#linkedin-learning #django

# Adding Login and Logout Pages

Creating the views

📁`home\views.py`
```python
...

from django.contrib.auth.views import LoginView, LogoutView

...

class LogoutInterfaceView(LogoutView):
    template_name = "home/logout.html"

class LoginInterfaceView(LoginView):
    template_name= "home/login.html"

...
```

Adding URL endpoints

📁`home\urls.py`
```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.HomeView.as_view(), name='home'),
    path('login', views.LoginInterfaceView.as_view(), name='login'),
    path('logout', views.LogoutInterfaceView.as_view(), name='logout'),
    path('signup', views.SignUpView.as_view(), name='signup'),
]
```

Login template

📁`home\templates\home\login.html`
```html
{% extends "base.html" %}

{% block content %}

<form method='post'>{% csrf_token %}

    {{form.as_p}}
    <input type='submit' class="btn btn-secondary"/>
    
</form>

{% endblock content %}
```

The default login URL redirect for Django is a profile page, which we do not have, so we will override it in the settings

📁`smartnotes\settings.py`
```python
...

LOGIN_REDIRECT_URL = '/smart/notes'
```

Logout template

📁`home\templates\home\logout.html`
```html
{% extends "base.html" %}

{% block content %}

<h1>Hope to see you soon!</h1>

{% endblock content %}
```

The problem here is that we are allowing a logged in user, which was the admin user I was using here to go to the signup page and create a new user. What we can do is make sure that only people that are not logged deemed can access the signup page. We can do this quite simply by overriding the get method. And redirecting the user if they are already logged in

📁`home\views.py`
```python
...

from django.shortcuts import redirect

...

class SignUpView(CreateView):
    form_class = UserCreationForm
    template_name = 'home/register.html'
    success_url = '/smart/notes'

    def get(self, request, *args, **kwargs):
        if self.request.user.is_authenticated:
            return redirect('notes.list')
        return super().get(request, *args, **kwargs)

...
```

# Finishing Touches

Adding a navbar to the base HTML

📁`static\templates\base.html`
```html
{% load static %}
<html>
    <head>
        <title>Smartnotes</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
        <link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}"/>
        </head>

        <body>
            <nav class='navbar navbar-dark bg-dark'>
                <div class='ms-auto'>
                    {% if user.is_authenticated %}
                    <a href="{% url "notes.list" %}" class="btn btn-outline-light">Home</a>
                    <a href="{% url "notes.new" %}" class="btn btn-outline-light">Create</a>
                    <form action="{% url 'logout' %}" method="POST" style="display: inline;">
                        {% csrf_token %}
                        <button type="submit" class="btn btn-outline-light">Logout</button>
                    </form>
                    {% else %}
                    <a href="{% url "login" %}" class="btn btn-outline-light">Login</a>
                    <a href="{% url "signup" %}" class="btn btn-outline-light">Signup</a>
                    {% endif %}
                </div>
            </nav>
            <div class="my-5 text-center container">
                {% block content %}
                {% endblock %}
            </div>
        </body>
</html>
```