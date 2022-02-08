# [Manager](https://docs.djangoproject.com/en/4.0/topics/db/managers/)

Topic covered
- [Rename Manager](#rename-manager)
- [Custom Manager](#custom-managers)
    - [Add Extra Manager](#add-extra-manager)
    - [Add Extra Manager Method](#add-extra-manager-methods)


A **Manager** is the interface through which database query operations are provided to Django models. At least one **Manager** exists for every model in a Django Application.

---
## Rename Manager

**NOTE:** By default, Django adds a **Manager** with the name `objects` to it's every django model class.
To rename the manager for a given model class, define a class attribute of type `models.Manager()` on the model For example:
```
from django.db import models

class Person(models.Model):
    #...
    people = models.Manager()
```

Now your manager is people not objects you can use it like `ClassName.manager.manager_methods`. So for this class `Person.people.all()`, `Person.people.get(**kwargs)`, `Person.people.filter(**kwargs)` etc.

---

## Custom Managers

### Add Extra Manager
To do this  first create class by extend `models.Manager` and inside this class override `get_queryset()` method 
```
class DahlBookManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(author='Roald Dahl')

# Then hook it into the Book model explicitly.
class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)

    objects = models.Manager() # The default manager.
    dahl_objects = DahlBookManager() # The Dahl-specific manager.
```
Work with extra manager `Book.dahl_objects.all()`, `Book.dahl_objects.filter(title='Matilda')`, `Book.dahl_objects.count()`




### Add Extra Manager Methods
To add extra manager methods create class extend `models.Manager` like so.
```
from django.db import models
from django.db.models.functions import Coalesce

class PollManager(models.Manager):
    def with_counts(self):
        return self.annotate(num_responses=Coalesce(models.Count("response"), 0)
     )
     
class OpinionPoll(models.Model):
    question = models.CharField(max_length=200)
    objects = PollManager()
```

In this `OpinionPoll` class we add a custom manager method named `with_counts`. We can use it `OpinionPoll.objects.with_counts()`.


### Add Extra Manager & Rename Default Manager
```
class AuthorManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(role='A')

class EditorManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(role='E')

class Person(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    role = models.CharField(max_length=1, choices=[('A', _('Author')), ('E', _('Editor'))])
    people = models.Manager()
    authors = AuthorManager()
    editors = EditorManager()
```
Here we rename `objects` manager to `people` manager and add extra `authors`, `editors` manager.
`Person.people.all()`
`Person.authors.all()`
`Person.editors.all()`


