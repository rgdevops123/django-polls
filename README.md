# django-polls
Django tutorial polls app

```
Django:

   MVC: Model View Controller
   MVT: Model View Template

Model: Interface to Data.
View:  Inteface that Users see.
Controller: Passes information between Model & View.

Note: Each model is a class with class variables that 
       represent fields in the database.
      Sets column names and data types to be created 
       in the database.


   *** Connect urls to functions. ***

pip install django

>>> import django

>>> django.get_version()
'2.2.6'

$ django-admin startproject sampsite

$ cd sampsite/

$ ls
manage.py  sampsite

$ tree
.
├── manage.py
└── sampsite
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py

1 directory, 5 files

$ cd ../sampsite

$ python3 manage.py runserver


$ vim sampsite/views.py
+++
from django.http import HttpResponse
 
def root_page(request):
    return HttpResponse("Root Home Page")
+++



         POLLS Application:

$ python3 manage.py startapp polls
         OR
$ git clone https://github.com/rgdevops123/django-polls.git

$ cd polls

$ ls
admin.py  apps.py  __init__.py  migrations  models.py  tests.py  views.py

$ tree
.
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py

1 directory, 7 files



$ vim settings.py
+++
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls.apps.PollsConfig',
]

TIME_ZONE = 'America/Los_Angeles'
+++


$ vim sampsite/urls.py
+++
from django.conf.urls import url
from django.conf.urls import include
from sampsite.views import root_page

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', root_page),
    url(r'^polls/', include('polls.urls')),
]
+++




$ python3 manage.py makemigrations polls

$ python3 manage.py sqlmigrate polls 0001

$ python3 manage.py migrate


   Add data to Database via Django Shell:

$ python3 manage.py shell

>>> from polls.models import Poll, Choice

>>> Poll.objects.all()
<QuerySet []>

>>> q = Poll(question="What's New?")

>>> q.save()

>>> q.id

>>> q.question
"What's New?"

>>> q.question = "What's Up?"

>>> q.save()

>>> Poll.objects.all()
<QuerySet [<Poll: What's Up?>]>

>>> Poll.objects.filter(id=1)
<QuerySet [<Poll: What's Up?>]>

>>> Poll.objects.filter(question__startswith='What')
<QuerySet [<Poll: What's Up?>]>

>>> Poll.objects.get(id=2)
Exception Raised!!!
   DoesNotExist
 
>>> Poll.objects.get(pk=1)
Search for primary key
<Poll: What's Up?>

   Show choices for matching question
>>> q.choice_set.all()
<QuerySet []>
 
   Add new choices
>>> q.choice_set.create(choice_text='Not Much', votes=0)                                           
<Choice: Not Much>

>>> q.choice_set.create(choice_text='The Sky', votes=0)                                            
<Choice: The Sky>

>>> q.choice_set.create(choice_text='The Clouds', votes=0)                                         
<Choice: The Clouds>


   Display choices
>>> q.choice_set.all()
<QuerySet [<Choice: Not Much>, <Choice: The Sky>, <Choice: The Clouds>]>
 
   Display number of choices
>>> q.choice_set.count()
3


   Delete a choice
>>> c = q.choice_set.filter(choice_text__startswith='The Clouds')
>>> c.delete()
(1, {'polls.Choice': 1})


   Admin Site:
$ python3 manage.py createsuperuser

   GOTO: http://localhost:8000/admin
```
