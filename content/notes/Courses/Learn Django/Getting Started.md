#django

A web framework written in Python, similar to Flask, for deploying websites quickly

Takes care of the difficult and routine parts of web development--authentication, database connection, CRUD (Create, Read, Update, Delete) operations, URL routing, forms, security

# Django Architecture

Uses a variant of MVC called MVT (Model View Template)

- **Models** are the data structure layer that represents the database schema
- **Views** are the business logic layer that receives a web request and returns a web response
- **Templates** are the presentation layer that displays information to the user

1. A user makes an HTTP Request, for example.com
2. A URLs processes it and assigns the correct View
3. The View combines a Template and data from a Model/Database to create an HTTP Response
4. The HTTP Response is returned to the user

# Django Project Structure

A single project has multiple **Apps**, each containing discrete functionality

Django ships with several built-in apps such as `admin`, `auth`, `sessions`, `messages`, `staticfiles`

# Models

Django's ORM (Object-Relational Mapper) means developers can define data models in Python and query them via a dynamic API, but you can still write SQL if needed. For example, this model defines an `Article` table in a newspaper app that contains three fields: `title`, `content`, and `pub_date`.

```python
# models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    pub_date = models.DateTimeField(auto_now_add=True)
```

# URLs

The python module `URLconf`, similar to a table of contents for the app, features precise mapping between URL patterns and your views.

```python
# urls.py
from django.urls import path

from .views import HomePageView, ArticleListView, ArticleDetailView

urlpatterns = [
    path("", HomePageView.as_view(), name="homepage"),
    path("articles/", ArticleListView.as_view(), name="article-list"),
    path("articles/<int:pk>", ArticleDetailView.as_view(), name="article-detail"),
]
```

In this example, three views are imported for a home page, an article list page, and an article detail page

Then, we define three paths that can define thousands or even millions of different webpages of articles

# Views

Views are the logic layer that receive web requests and return web responses

```python
# views.py
from django.views.generic import TemplateView, ListView, DetailView
from .models import Article

class HomePageView(TemplateView):
    template_name = "home.html"

class ArticleListView(ListView):
    model = Article
    template_name = "article_list.html"

class ArticleDetailView(DetailView):
    model = Article
    template_name = "article_detail.html"
```

This snippet is all the code we need to use built-in views to display a template called `home.html`, list all articles in a template called `article_list.html`, and display a detail view of a single article in `article_detail.html`

# Templates

A template is a text file, typically HTML, that contains variables replaced with values when the template is evaluated and built-in tags and filters that control the logic of the template

A simple template file that displays all articles in the database would look as follows:

```html
<!-- article_list.html -->
<h1>All Articles</h1>
{% for article in article_list %}
  <div>
    <h2>{{ article.title }} | {{ article.pub_date }}</h2>
    <p>{{ article.content }}</p>
  </div>
{% endfor %}
```

And a template file to display a single article could look like this:

```python
<!-- article_detail.html -->
<h1>{{ article.title }} {{ article.pub_date }}</h1>
<p>{{ article.content }}</p>
```

