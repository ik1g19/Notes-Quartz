#templating 

---
# Creating a Dynamic Template

Now we create another view to start displaying notes

📁`notes\views.py`
```python
from django.shortcuts import render
from .models import Notes

def list(request):
    all_notes = Notes.objects.all()
    return render(request, 'notes/notes_list.html', {'notes': all_notes})
```

Now we create a new `urls` file
📁`notes\urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('notes', views.list),
]
```

This creates the notes endpoint

Again we have to add this on the `urls.py` on smartnotes

📁`smartnotes\urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('home.urls')),
    path('smart/', include('notes.urls')),
]
```

Finally, we need to create the notes template

📁`notes\templates\notes\notes_list.html`
```html
<html>
    <h1>These are the notes</h1>

    <ul>
        {% for note in notes %}
            <li>{{note.title}}</li>
        {% endfor %}
    </ul>
</html>
```

Everything between curly brackets is [[notes/Courses/Django Training/Starting your Django Project#^e6a487|DTL]] logic

`http://127.0.0.1:8000/smart/notes` now dynamically renders all the notes in the database

![[Images/Pasted image 20240913220524.png|400]]

# Display Content of a Single Note

Now we create a view for note details, since currently only the titles are displayed

`📁notes\views.py`
```python
from django.shortcuts import render
from django.http import Http404

from .models import Notes

def list(request):
    all_notes = Notes.objects.all()
    return render(request, 'notes/notes_list.html', {'notes': all_notes})

def detail(request, pk):
	try:
		note = Notes.objects.get(pk=pk)
	except Notes.DoesNotExist:
		raise Http404("Note doesn't exist")
	return render(request, 'notes/notes_detail.html', {'note': note})
```
^list-function-based-view

We pass the private key as `pk`

We also import `Http404` so that we can throw an exception and render a 404 page if the user tries to access a note which does not exist

Now we need to create the template

📁`notes\templates\notes\notes_detail.html`
```html
<html>
    <h1>{{note.title}}</h1>

    <p>{{note.text}}</p>
</html>
```

Now we need to add the url and allow it to let us pass information through, in this case it will be which note to load

We are telling the url to accept a variable called `pk` which is an integer

📁`notes\urls.py`
```python
from django.urls import path
from . import views
urlpatterns = [
    path('notes', views.NotesListView.as_view()),
    path('notes/<int:pk>', views.NotesDetailView.as_view()),
]
```

# Introduction to Django Class-Based Views

Class based views are extensive classes that implement typical view behaviour

First we will change our function-based views to class based views in `home\views.py`

📁`home\views.py`
```python
from django.shortcuts import render
from django.http import HttpResponse
from datetime import datetime
from django.contrib.auth.decorators import login_required
from django.views.generic import TemplateView
from django.contrib.auth.mixins import LoginRequiredMixin

class HomeView(TemplateView):
    template_name = 'home/welcome.html'
    extra_context = {'today': datetime.today()}

class AuthorizedView(LoginRequiredMixin, TemplateView):
    template_name = 'home/authorized.html'
    login_url = '/admin'
```

We import `TemplateView` to create our class-based views, each class inherits from `TemplateView`

To add back authentication functionality we use a `LoginRequiredMixin`

Function-based view from earlier for comparison

![[notes/Courses/Django Training/Django Built in User Management#^function-based-view|Django Built in User Management]]

# A bit more on Class-Based Views

We will now create class-based views for the notes app

📁`notes\views.py`
```python
from django.shortcuts import render
from django.http import Http404
from django.views.generic import DetailView, ListView

from .models import Notes

class NotesListView(ListView):
    model = Notes
    context_object_name = "notes"
    template_name = "notes/notes_list.html"

class NotesDetailView(DetailView):
    model = Notes
    context_object_name = "note"
```

Here is how the function based view for this used to look

![[#^list-function-based-view]]

`DetailView` already handles the exception, so it does not need to be included