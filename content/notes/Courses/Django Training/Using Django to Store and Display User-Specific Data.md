#linkedin-learning #django 

# How Models relate to each other

So far we have two tables in the database

We are going to add a foreign key between the `Notes` and `User` table to remember which users created which notes

![[Images/Pasted image 20241015223930.png|600]]

We now import and add the `User` model and add the foreign key

The first parameter is the model we want to create a link with

The second parameter is how we define what happens to the note if the user associated with it is deleted

The third parameter is how we will identify this relationship

📁`notes\models.py`
```python
from django.db import models
from django.contrib.auth.models import User

# Create your models here.
class Notes(models.Model):
    title = models.CharField(max_length=200)
    text = models.TextField()
    created = models.DateTimeField(auto_now_add=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name="notes")
```

When we try to create our migrations we will get an error as we are defining that ever note needs to be associated with a user, but our database is already populated with notes without users

```
python manage.py makemigrations
```

![[Images/Pasted image 20241015224616.png]]

What we can do is provide a default value for all existing database entries to fill this column, which is the admin id `1`

Now we can apply migrations

```
python manage.py migrate
```

You can now see all the notes belong to the admin user by using the Django Shell

![[Images/Pasted image 20241015224840.png|400]]

# Displaying only the Logged in User Data

This `login_url` means that if a user tried to access the list view and is not logged in, they will be redirected to the `/admin` instead of seeing a `404`

We override `self.get_queryset` so that only the logged in users notes are returned

📁`notes\views.py`
```python
...

from django.contrib.auth.mixins import LoginRequiredMixin

...

class NotesListView(LoginRequiredMixin, ListView):
    model = Notes
    context_object_name = "notes"
    template_name = "notes/notes_list.html"
    login_url = "/login"

    def get_queryset(self):
        return self.request.user.notes.all()

...
```

# Adding a new Notes after Foreign Key

The problem is that we don't say in the form to consider the logged in user as the author of that note

📁`notes\views.py`
```python
class NotesCreateView(LoginRequiredMixin, CreateView):
    model = Notes
    success_url = '/smart/notes'
    form_class = NotesForm
    login_url = "/admin"

    def form_valid(self, form):
        self.object = form.save(commit=False)
        self.object.user = self.request.user
        self.object.save()
        return HttpResponseRedirect(self.get_success_url())
```

The data is sent by the user, passed inside the form, which asks a simple question: is this data valid. To see if the data is valid, the form would call a couple of methods that have the title started with clean. So clean title, clean text, like the one we changed before. If something is wrong, the method is valid returns false, and the class-based view will raise an exception. On the other hand, if all checks clear, the data is stored in a variable called clean data. And when you call `form.save`, that will save the object directly in the database. And that's it. It all's happened very smoothly

![[Images/Pasted image 20241015225658.png|500]]

So what happens here is that when we pass title and text to the form, the method is valid returns through. Then the form valid method will call the save and we will try to save to the database, but although the form is returning is valid, is equal through the database is forbidding us to try to save a note without a user. That's where we get our error

![[Images/Pasted image 20241015225802.png|200]]

What we did here was get in the middle of it so we can inject the logged user as part of the object. We do this by passing the attribute commit equals false, that creates the object, but doesn't save it to the database. Then we have the object when we insert the user, and then we call save, successfully saving the note with that user to the database

![[Images/Pasted image 20241015225901.png|400]]