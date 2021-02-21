![GaffCo Consulting Logo](https://github.com/NaoiseGaffney/CI-PTD-II/blob/development/Documentation/Gaffco_Logo.png)

# GaffCo Consulting Professional Training and Development: Professional Communication and Presentation Skills E-Commerce Website

Professional Communication and Presentation Skills - 4th Milestone Project for the Code Institute's Diploma in Full Stack Development. Project requirements: HTML 5, CSS 3, JavaScript, Python 3, Django, PostgreSQL, and API's. This project website is an e-commerce site for a Professional Communications and Presentation Skills Company (Sole Trader) called GaffCo Consulting.
## GitHub

1. Create GitHub Repository using the CI Full Template.
2. Create a development branch (master + development).

## Visual Studio Code

### Configure Visual Studio Code environment

3. New Window.
4. Clone Repository -> GitHub -> [CI-PTD-II](https://github.com/NaoiseGaffney/CI-PTD-II).
5. Select development branch.
6. Create a virtual Python environment - Terminal: `python3 -m venv .venv`
7. Activate virtual Python environment - Terminal: `source .venv/bin/activate`
8. Install Django 3.1 - Terminal: `pip3 install Django`
9. Upgrade pip - Terminal: `pip3 install pip --upgrade`
10. Check Django version - Terminal: `python3 -m django --version` = 3.1.7
11. Update `.gitignore` to include `.venv`.
### Create the Initial Django Project

12. Create a Django **Project** called "PTD" - Terminal: `django-admin startproject PTD .` (created in the current folder)
13. Verify that the initial Django project works - Terminal: `python3 manage.py runserver 8000`, `http://127.0.0.1:8000/`

## Django Migrations (Version Control System for the Database Schema)'

> *migrate*, which is responsible for applying and unapplying migrations.
>
> *makemigrations*, which is responsible for creating new migrations based on the changes you have made to your models.
>
> *sqlmigrate*, which displays the SQL statements for a migration.
>
> *showmigrations*, which lists a project’s migrations and their status.

Link: https://docs.djangoproject.com/en/3.1/topics/migrations/
14. Apply the initial Django migrations: `python3 manage.py migrate`, add `--plan`to validate before commit.
15. Create Django Admin superuser account: `python3 manage.py createsuperuser`, `gaff`, `naoise.gaff.gaffney@gmail.com`, `password....`

## Django AllAuth Application

Link: https://django-allauth.readthedocs.io/en/latest/

Similar to the Flask-User extension.

16. Install Django AllAuth: `pip3 install django-allauth`
17. Configure AllAuth in *settings.py* based on the information: `https://django-allauth.readthedocs.io/en/latest/installation.html`
18. Add AUTHENTICATION_BACKENDS:

```
AUTHENTICATION_BACKENDS = [
    # Needed to login by username in Django admin, regardless of `allauth`
    'django.contrib.auth.backends.ModelBackend',

    # `allauth` specific authentication methods, such as login by e-mail
    'allauth.account.auth_backends.AuthenticationBackend',
]
```

19. Add INSTALLED_APPS:

```
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
```

20. Add AUTHENTICATION_BACKEND:

```
SITE_ID = 1
```

21. Add accounts URL to *urls.py*: `path('accounts/', include('allauth.urls')),` and import include: `from django.urls import path, include`
22. Update the DB Schema: `python3 manage.py migrate` as we added apps.
23. Run Server: `python3 manage.py runserver`
24. Login to admin interface and update the site to `gaffcoconsulting.example.com` and the display name to `GaffCo Consulting Professional Training`.
25. In settings.py add AllAuth configuration for e-mail settings:

```
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend' # Log E-Mails to Console

ACCOUNT_AUTHENTICATION_METHOD = 'username_email'
ACCOUNT_EMAIL_REQUIRED = True
ACCOUNT_EMAIL_VERIFICATION = 'mandatory'
ACCOUNT_SIGNUP_EMAIL_ENTER_TWICE = True
ACCOUNT_USERNAME_MIN_LENGTH = 4
LOGIN_URL = '/accounts/login/'
LOGIN_REDIRECT_URL = '/'
```

### Requirements.txt and Templates Directories

26. `pip3 freeze > requirements.txt`
27. Create templates/allauth: `mkdir templates`and `mkdir templates/allauth`
28. Stage -> Commit -> Synch/Push

### Base Templates

29. Copy templates to allow modification with Materialize CSS 1.0.0: `cp -r .venv/lib/python3.8/site-packages/allauth/templates/* templates/allauth`
30. Create a template/base.html. Use Materialize CSS 1.0.0 and add blocks to `base.html`

### Create Django Home Application

31. Create a Django **Application** called "home" - Terminal: `python3 manage.py startapp home`
32. Create Home Templates directories home/templates/home.
33. Create index.html.
34. Edit home/views.py to add -> home/index.html
35. Create and edit home/urls.py.
36. Update Project urls.py to include the new Home URL.
37. Add Home to installed apps in Project settings.py.
38. Add both to the TEMPLATES DIRS in settings.py.

### Configure static and media for Django

39. Create the media folder in the Project root.
40. Create the static folder with the following sub-folders: scripts (js), scripts/vendors (vendor js), styles (css).
41. Configure 'settings.py' and 'urls.py' to accommodate the static and media folders.

```

STATIC_URL = '/static/'

*STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

MEDIA_URL = '/media/'

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')*

```

```
from django.contrib import admin
from django.urls import path, include
*from django.conf import settings*
*from django.conf.urls.static import static*

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/', include('allauth.urls')),
    path('', include('home.urls')),
] *+ static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)*
```

#### Create a Django Application as a Parent of the Django Project

13. Create a Django **Application** called "todo" - Terminal: `python3 manage.py startapp todo`
14. Add the first **View** in "polls/views.py.
15. Create the first **URL** in "polls/urls.py" (create the file).
16. Point the root URLconf at the "polls/urls.py".
17. Verify that the new URL's work -  Terminal: `python manage.py runserver`, `http://127.0.0.1:8000/polls/`

#### Database Setup

18. Update "mysite/mysite/settings.py" to use the correct database binding, default is "sqlite3".
19. Update `TIME_ZONE = 'GMT'`.
20. Create the **Database** tables for the `INSTALLED_APPS` in "settings.py" - Terminal: `python manage.py migrate`

#### Creating Models

21. Update "polls/models.py" with the models (Question and Choice).

#### Activating Models (Change the Models in "models.py", run `python manage.py makemigrations` to create migrations for those changes, and `python manage.py migrate` to apply those changes to the database.)

22. Add `polls.apps.PollsConfig` to "mysite/mysite/settings.py".
23. Store the Models as migrations - Terminal: `python manage.py makemigrations polls`
24. (Optional) View, to verify, the SQL statements that are used by `migrate` to create the database tables - Terminal: `python manage.py sqlmigrate polls 0001`
25. Create the **Database** tables for the new Models - Terminal: `python manage.py migrate`

#### Playing with the API

26. `python manage.py shell`, shell ensures that manage.py sets the `DJANGO_SETTINGS_MODULE` environment variable.
27. Add...

```

import datetime
from django.utils import timezone
...
    def __str__(self):
        return self.question_text
...
    def __str__(self):
            return self.choice_text
...
    def was_published_recently(self):
            return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

```

#### Django Admin

28. Create an admin user - Terminal: `python manage.py createsuperuser`
29. Verify that the Admin URL works -  Terminal: `python manage.py runserver`, `http://127.0.0.1:8000/admin/`
30. Make the poll application modifiable in Django Admin in "polls/admin.py".

#### Views and URL's

31. Update "polls/views.py" with more **Views**.
32. Update "polls/urls.py" with more **URL's** linked to the **Views**.

URL's -> Views -> Models

**polls/urls.py**

````

from django.urls import path

from . import views

urlpatterns = [
    # ex: /polls/
    path('', views.index, name='index'),
    # ex: /polls/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # ex: /polls/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # ex: /polls/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),
]

````

**polls/views.py**

````

from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")

def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)

````
