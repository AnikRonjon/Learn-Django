# [Manager](https://docs.djangoproject.com/en/4.0/topics/db/managers/)

A **Manager** is the interface through which database query operations are provided to Django models. At least one **Manager** exists for every model in a Django Application.

---
## Manager names

**NOTE:** By default, Django adds a **Manager** with the name `objects` to it's every django model class.
To rename the manager for a given model class, define a class attribute of type `models.Manager()` on the model For example:
```
from django.db import models

class Person(models.Model):
    #...
    people = models.Manager()
```
Now your manager is people not objects you can use it like `ClassName.manager`. So for this class `Person.people.all()`, `Person.people.get(**kwargs)`, `Person.people.filter(**kwargs)` etc.
---


