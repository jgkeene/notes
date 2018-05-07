# Django tutorial

```bash
# to install package to user only
pip3 install --user PACKAGE
```

```bash
# to get started with Django on a virtualenv
cd ~/local/virtualenvs/
virtualenv --python python3 django/
. django/bin/activate
```


```bash
# exporting your required packages
pip3 freeze > requirements.txxt
# other people can install your requirements
pip3 install -r requirements.txt
```

# Part 1

`django-admin startproject mysite`
`python manage.py runserver`


`python manage.py startapp polls`
```python
# vim polls/views.py: INSERT...
from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```


```python
# touch polls/urls.py
# vim polls/urls.py: INSERT...
from django.conf.urls import url
from . import views
urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```

```python
# vim mysite/urls.py: INSERT...
from django.conf.urls import include, url
from django.contrib   import admin
urlpatterns = [
    url(r'^polls/', include('polls.urls')),   # point the root URLconf at the polls.urls module
    url(r'^admin/', admin.site.urls),
]
```

# Part 2
- setup the database
- create your first model
- get a quick introduction to Django’s automatically-generated admin site


```python
python manage.py migrate

# looks in my_webservesr/settings.py, INSTALLED_APPS setting creates any necessary database tables
# according to the database settings in your mysite/settings.py file
```

## Creating models
Now we’ll define your models – essentially, your database layout

- __Philosophy:__ A ***model*** is the *single, definitive source of truth about your data*
- It contains the essential fields and behaviors of the data you’re storing.
- Django follows the DRY Principle: The goal is to define your data model in one place and automatically derive things from it.
- migrations are entirely derived from your models file, and are essentially just a history that Django can roll through to update your database schema to match your current models.
- In our simple poll app, we’ll create two models:
  1. Question
  2. Choice.
- A Question has a question and a publication date.
- A Choice has two fields: the text of the choice and a vote tally.
- Each Choice is associated with a Question.

```python
# vim polls/models.py: INSERT...
from django.db import models
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')
class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

- The code is straightforward. Each model is represented by a class that subclasses django.db.models.Model.
- Each model has a number of class variables, each of which represents a database field in the model.
- Each field is represented by an instance of a Field class – e.g., CharField for character fields and
- DateTimeField for datetimes. This tells Django what type of data each field holds.
- The name of each Field instance (e.g. question_text or pub_date) is the field’s name, in machine-friendly
- format. You’ll use this value in your Python code, and your database will use it as the column name.
- You can use an optional first positional argument to a Field to designate a human-readable name. That’s used
- in a couple of introspective parts of Django, and it doubles as documentation. If this field isn’t provided, Django
- will use the machine-readable name. In this example, we’ve only defined a human-readable name for Question.
- pub_date. For all other fields in this model, the field’s machine-readable name will suffice as its human-readable
- name.
- Some Field classes have required arguments. CharField, for example, requires that you give it a max_length.
- That’s used not only in the database schema, but in validation, as we’ll soon see.
- A Field can also have various optional arguments; in this case, we’ve set the default value of votes to 0.
- Finally, note a relationship is defined, using ForeignKey. That tells Django each Choice is related to a single
- Question. Django supports all the common database relationships: many-to-one, many-to-many, and one-to-one.


## Activating models
That small bit of model code gives Django a lot of information. With it, Django is able to:
- Create a database schema (CREATE TABLE statements) for this app.
- Create a Python database-access API for accessing Question and Choice objects.
- But first we need to tell our project that the polls app is installed.
- __Philosophy:__ Django apps are “pluggable”: You can use an app in multiple projects, and you can distribute apps, because they don’t have to be tied to a given Django installation.


```python
# vim mysite/settings.py: INSERT

INSTALLED_APPS = [
  'polls.apps.PollsConfig',   # <------------
  'django.contrib.admin',
  'django.contrib.auth',
  'django.contrib.contenttypes',
  'django.contrib.sessions',
  'django.contrib.messages',
  'django.contrib.staticfiles',
]
```

- Now Django knows to include the polls app. Let’s run another command:

```python
python manage.py makemigrations polls
```
- By running makemigrations, you’re telling Django that you’ve made some changes to your models
- (in this case you’ve made new ones) and that you’d like the changes to be stored as a migration
- Migrations are how Django stores changes to your models (and thus your database schema)

- let’s see what SQL that migration would run
- The sqlmigrate command takes migration names and returns their SQL:

```python
python manage.py sqlmigrate polls 0001
```
- If you’re interested, you can also run `python manage.py check`
- this checks for any problems in your project without making migrations or touching the database.

- Now, run migrate again to create those model tables in your database:

```python
python manage.py migrate
```

- The `migrate` command takes all the migrations that haven’t been applied
- (Django tracks which ones are applied us-
 ing a special table in your database called django_migrations)
- django runs them against your database - essentially,
 synchronizing the changes you made to your models with the schema in the database.
- Migrations are very powerful and let you change your models over time, as you develop your project, without the need
 to delete your database or tables and make new ones
- it specializes in upgrading your database live, without losing
 data.
- we’ll cover them in more depth in a later part of the tutorial, but for now, remember the three-step guide to
 making model changes:
  1. Change ge your models (in models.py)
  2. Run python manage.py makemigrations to create migrations for those changes
  3. Run python manage.py migrate to apply those changes to the database.

## Playing around with the API - w/ iPython

```bash
python ./manage.py shell -i ipython
```


```python
import django
django.setup()

from polls.models import Question, Choice
Question.objects.all()
# returns -> <QuerySet []>

from django.utils import timezone
q = Question(question_text="What's new?", pub_date=timezone.now())

# Save the object into the database. You have to call save() explicitly.
q.save()

# Access model field values via Python attributes.
q.question_text
q.pub_date

# Change values by changing the attributes, then calling save().
q.question_text = "What's up?"
q.save()

# objects.all() displays all the questions in the database.
Question.objects.all()
```


 Let's add a (in the polls/models.py file) to both Question and Choice:

```python
# vim polls/models.py: INSERT...
class Question(models.Model):
  # ...
    def __str__(self):
        return self.question_text

class Choice(models.Model):
  # ...
    def __str__(self):
        return self.choice_text
```

- It’s important to add __str__() methods to your models, not only for your own convenience when dealing with the interactive prompt
- but also because objects’ representations are used throughout Django’s automatically-generated admin


- Now let’s add another custom method, just for demonstration:
```python
# vim polls/models.py: INSERT...
import datetime
from django.db import models
from django.utils import timezone
class Question(models.Model):
  # ...
  def was_published_recently(self):
    return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```

First we’ll need to create a user who can login to the admin site. Run the following command:
```python
python manage.py createsuperuser
```


## Writing more views
- Now let’s add a few more views to polls/views.py. These views are slightly different, because they take an
argument:

```python
# vim polls/views.py: INSERT...

def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)
def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)
def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

Wire these new views into the polls.urls module by adding the following url() calls:





Because it’s convenient, let’s use Django’s own database API, which we covered in Tutorial 2. Here’s one stab at
a new index() view, which displays the latest 5 poll questions in the system, separated by commas, according to
publication date:
polls/views.py
from django.http import HttpResponse
from .models import Question
def index(request):
latest_question_list = Question.objects.order_by('-pub_date')[:5]
output = ', '.join([q.question_text for q in latest_question_list])
return HttpResponse(output)
# Leave the rest of the views (detail, results, vote) unchanged

