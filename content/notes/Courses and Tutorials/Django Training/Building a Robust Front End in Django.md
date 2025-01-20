#django #python #linkedin-learning

---

# Static Files in Django

We need to create space where we are going to store all static files such as CSS, JavaScript files, images and videos

After creating a static folder at the root, we need to tell Django where it is

📁`smartnotes\settings.py`
```python
...
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/5.1/howto/static-files/

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
...
```

We create a CSS styling file

📁`static\css\style.css`
```css
.note-li {
    color: red;
}
```

Styling can then be used in Django templates in the following way

📁`notes\templates\notes\notes_list.html`
```html
{% load static %}

<html>
	<head>
		<link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}" />
	</head>
    <h1>These are the notes</h1>

    <ul>
	    {% for note in notes %}
		    <li class="note-li">{{note.title}}</li>
		{% endfor %}
	</ul>
</html>
```
# How to Set up a Base HTML for every Django Template


It would be exhaustive to add all the CSS links to all the templates we have in our apps

Create a templates folder in the static folder and a `base.html

📁`static\templates\base.html`
```html
{% load static %}
<html>
    <head>
        <title>Smartnotes</title>
        <link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}">
        </head>

        <body>
			{% block content %}
			{% endblock %}
        </body>
</html>
```

Now to add our base template to another file, we can do this

📁`notes\templates\notes\notes_list.html`
```html
{% extend "base.html" %}

{% block content %}
    <h1>These are the notes</h1>

    <ul>
	    {% for note in notes %}
		    <li class="note-li">{{note.title}}</li>
		{% endfor %}
	</ul>
{% endblock %}
```

In order to use our base template we have to add it to the `settings` file

📁`smartnotes\settings.py`
```python
...
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            BASE_DIR / 'static/templates',
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
...
```

![[Images/Pasted image 20240916214713.png|600]]

Templating allows us to keep all configuration in a single place while keeping the code for each webpage as simple as possible
# Let's add Some Style

We will now use a CSS framework, in this case [[notes/Misc/Bootstrap|Bootstrap]]

📁`static\templates\base.html`
```html
{% load static %}
<html>
    <head>
        <title>Smartnotes</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">
        </head>

        <body>
            <div class="my-5 text-center container">
                {% block content %}
                {% endblock %}
            </div>
        </body>
</html>
```

Now we have linked the bootstrap framework we can use the styling in our elements

As seen in `<div class="my-5 text-center container">`

We will add a button to the homepage that will lead us to the rest of the notes

📁`home\templates\home\welcome.html`
```html
{% extends "base.html" %}

{% block content %}
    <h1>Welcome to SmartNotes!</h1>
    <p>Today is {{today}}</p>
    <a href="{% url 'notes.list' %}" class="btn btn-primary">Check out these smart notes!</a>
{% endblock %}
```

In order to tell Django which endpoint to link `{% url 'notes.list' %}` to, we have to go to `notes\urls.py`

📁`notes\urls.py`
```python
from django.urls import path
from . import views
urlpatterns = [
    path('notes', views.NotesListView.as_view(), name="notes.list"),
    path('notes/<int:pk>', views.NotesDetailView.as_view(), name="notes.detail"),
]
```

We use `name=""` to give each endpoint a name so Django can dynamically define each endpoint that we want to point to

We now add some bootstrap styling to the notes list template

📁`notes\templates\notes\notes_list.html`
```html
{% extends "base.html" %}

{% block content %}

    <h1 class="my-5">These are the notes</h1>

    <div class = "row row-cols3 g-2">
        {% for note in notes %}
        <div class="col">
            <div class="p-3 border">
                <a href="{% url 'notes.detail' pk=note.id %}" class="text-dark text-decoration-non">
                    <h3>{{note.title}}</h3>
                </a>
                {{note.text|truncatechars:10}}
            </div>
        </div>
        {% endfor %}
    </div>
        
    

{% endblock %}
```

Styling `notes_detail.html`

📁`notes\templates\notes\notes_detail.html`
```html
{% extends "base.html" %}

{% block content %}
<div class="border round">
    <h1 class="my-5">{{note.title}}</h1>
    <p>{{note.text}}</p>
</div>
{% endblock %}
```