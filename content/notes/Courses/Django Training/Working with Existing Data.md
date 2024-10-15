#linkedin-learning #django

# Updating Data

Add update view

📁`notes\views.py`
```python
...

from django.views.generic import CreateView, DetailView, ListView, UpdateView

class NotesUpdateView(UpdateView):
    model = Notes
    success_url = '/smart/notes'
    form_class = NotesForm
    
...
```

Add `edit` URL endpoint to `urls`

📁`notes\urls.py`
```python
from django.urls import path
from . import views
urlpatterns = [
    path('notes', views.NotesListView.as_view(), name="notes.list"),
    path('notes/<int:pk>', views.NotesDetailView.as_view(), name="notes.detail"),
    path('notes/<int:pk>/edit', views.NotesUpdateView.as_view(), name="notes.update"),
    path('notes/new', views.NotesCreateView.as_view(), name="notes.new"),
]
```

In 📁`notes\templates\notes\notes_form.html`, we are currently hard programming the URL into the form, so editing will not work

![[notes/Courses/Django Training/Django Forms#^hardcoded]]

Instead, we can leave the action value blank so that the form will use the appropriate URL

We also add a cancel button

📁`notes\templates\notes\notes_form.html`
```html
{% extends 'base.html' %}

{% block content %}

<form method='POST'>{% csrf_token %}
    {{ form }}
    <button type="submit" class="btn btn-primary my-5">Submit</button>
</form>

{% if form.errors %}
<div class="alert alert-danger my-5">
    {{form.errors.title.as_text}}
</div>
{% endif %}
<a href="{% url 'notes.list' %}" class="btn btn-secondary">Cancel</a>

{% endblock %}
```

We also add an edit button to each note view

📁`notes\templates\notes\notes_detail.html`
```python
{% extends "base.html" %}

{% block content %}
<div class="border round">
    <h1 class="my-5">{{note.title}}</h1>
    <p>{{note.text}}</p>
</div>

<a href="{% url 'notes.list' %}" class="btn btn-secondary">Back</a>
<a href="{% url 'notes.update' pk=note.id %}" class="btn btn-secondary">Edit</a>
{% endblock %}
```

# Deleting Data

We create a new delete view

📁`notes\views.py`
```python
...

from django.views.generic.edit import DeleteView

class NotesDeleteView(DeleteView):
    model = Notes
    success_url = '/smart/notes'
    template_name = 'notes/notes_delete.html'
    
...
```

Add the URL endpoint

📁`notes\urls.py`
```python
from django.urls import path
from . import views
urlpatterns = [
    path('notes', views.NotesListView.as_view(), name="notes.list"),
    path('notes/<int:pk>', views.NotesDetailView.as_view(), name="notes.detail"),
    path('notes/<int:pk>/edit', views.NotesUpdateView.as_view(), name="notes.update"),
    path('notes/<int:pk>/delete', views.NotesDeleteView.as_view(), name="notes.delete"),
    path('notes/new', views.NotesCreateView.as_view(), name="notes.new"),
]
```

Create the delete template

📁`notes\templates\notes\notes_delete.html`
```html
{% extends "base.html" %}

{% block content  %}
<form method='post'>{% csrf_token %}
    <p>Are you sure you want to delete "{{notes.title}}"</p>
    <p>This action can't be undone</p>

    <input type="submit" class="btn btn-danger" value="Confirm"/>
</form>
{% endblock  %}
```

And add a delete button

📁`notes\templates\notes\notes_detail.html
```html
{% extends "base.html" %}

{% block content %}
<div class="border round">
    <h1 class="my-5">{{note.title}}</h1>
    <p>{{note.text}}</p>
</div>

<a href="{% url 'notes.list' %}" class="btn btn-secondary">Back</a>
<a href="{% url 'notes.update' pk=note.id %}" class="btn btn-secondary">Edit</a>
<a href="{% url 'notes.delete' pk=note.id %}" class="btn btn-secondary">Delete</a>
{% endblock %}
```