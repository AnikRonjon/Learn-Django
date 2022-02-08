# [Manager](https://docs.djangoproject.com/en/4.0/topics/db/managers/)

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

### Adding extra manager methods

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

---




