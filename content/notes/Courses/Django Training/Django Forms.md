
#django #bootstrap 

---
# Create a Webpage

When building a system, every model we create should support **CRUD** (Create, Read, Update and Delete)

So far we have implemented a retrieve method by having an endpoint to get the details of a particular note

To fully support the model we need to handle all the other 3 operations as well

First we import `CreateView` from `Django.views` and make a new note creation view

📁`notes\views.py`
```python
from django.shortcuts import render
from django.http import Http404
from django.views.generic import CreateView, DetailView, ListView

from .models import Notes

class NotesCreateView(CreateView):
    model = Notes
    fields = ['title', 'text']
    success_url = '/smart/notes'

class NotesListView(ListView):
    model = Notes
    context_object_name = "notes"
    template_name = "notes/notes_list.html"

class NotesDetailView(DetailView):
    model = Notes
    context_object_name = "note"
```

We want to redirect the user to the list of existing notes so they can see the note they just created, this is the `success_url`

The `fields` are the attributes from the model that we allow a user to fill

Next we add the endpoint

📁`notes\urls.py`
```python
from django.urls import path
from . import views
urlpatterns = [
    path('notes', views.NotesListView.as_view(), name="notes.list"),
    path('notes/<int:pk>', views.NotesDetailView.as_view(), name="notes.detail"),
    path('notes/new', views.NotesCreateView.as_view(), name="notes.new"),
]
```

Then the last thing to create is the template

📁`notes\templates\notes\notes_form.html`
```html
{% extends 'base.html' %}

{% block content %}

<form action="{% url "notes.new" %}" method='POST'>
    {{ form }}
    <button type="submit" class="btn btn-primary my-5">Submit</button>
</form>

{% endblock %}
```

To send information back to the server we use a `form` tag and use the `url` action along with the new endpoint, the method needs to be `POST` as we are sending information back to the server

Django already knows what type of data each attribute expects, so it creates an appropriate HTML tag to receive it

# Understanding how Django handles Security in POSTs

If you try using the form in its current state it will not work

You need to add a [[notes/Uni Content/Web and Cloud Based Security/Yet More Vulnerabilities#Cross-Site Request Forgery|CSRF]] token

📁`notes\templates\notes\notes_form.html`
```html
{% extends 'base.html' %}

{% block content %}

<form action="{% url "notes.new" %}" method='POST'>{% csrf_token %}
    {{ form }}
    <button type="submit" class="btn btn-primary my-5">Submit</button>
</form>

{% endblock %}
```

# Powerful Validation with Minimal Work

First we create `forms.py` and the `NotesForm` class

📁`notes\forms.py`
```python
from django import forms
from django.core.exceptions import ValidationError

from .models import Notes

class NotesForm(forms.ModelForm):
    class Meta:
        model = Notes
        fields = ('title', 'text')

    def clean_title(self):
        title = self.cleaned_data['title']
        if 'Django' not in title:
            raise forms.ValidationError("Only accepting notes about Django")
        return title
```

The `cleaned_data` is a dictionary and is returned by the form

And remove the fields attribute from `NotesCreateView` and instead pass a `form_class`, which is the class we just created

📁`notes\views.py`
```python
from django.shortcuts import render
from django.http import Http404
from django.views.generic import CreateView, DetailView, ListView

from .models import Notes
from .forms import NotesForm

class NotesCreateView(CreateView):
    model = Notes
    success_url = '/smart/notes'
    form_class = NotesForm

class NotesListView(ListView):
    model = Notes
    context_object_name = "notes"
    template_name = "notes/notes_list.html"

class NotesDetailView(DetailView):
    model = Notes
    context_object_name = "note"
```

Django renders error such as the one raised in `raise forms.ValidationError("Only accepting notes about Django")` as an unordered list of class `errorlist`

To control the styling of this, we hide the original Django list

📁`static\css\style.css`
```css
ul.errorlist {display: none}
```

And we add this conditional block to our form template to render the errors using [[notes/Misc/Bootstrap|Bootstrap]]

📁`notes\templates\notes\notes_form.html`
```html
{% extends 'base.html' %}

{% block content %}

<form action="{% url "notes.new" %}" method='POST'>{% csrf_token %}
    {{ form }}
    <button type="submit" class="btn btn-primary my-5">Submit</button>
</form>

{% if form.errors %}
<div class="alert alert-danger my-5">
    {{form.errors.title.as_text}}
</div>
{% endif %}

{% endblock %}
```

# Forms are Useful for Layout as Well

This is how the original template makes the form look

![[Images/Pasted image 20240923201651.png]]

We can control the styling through the backend by adding widgets and labels

📁`notes\forms.py`
```python
from django import forms
from django.core.exceptions import ValidationError

from .models import Notes

class NotesForm(forms.ModelForm):
    class Meta:
        model = Notes
        fields = ('title', 'text')
        widgets = {
            'title' : forms.TextInput(attrs={'class': 'form-control my-5'}),
            'text': forms.Textarea(attrs={'class': 'form-control my-5'})
        }
        labels = {
            'text' : 'Write your thoughts here'
        }

    def clean_title(self):
        title = self.cleaned_data['title']
        if 'Django' not in title:
            raise forms.ValidationError("Only accepting notes about Django")
        return title
```



![[Images/Pasted image 20240923201715.png]]