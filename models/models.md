# Django Models

### Queryset API [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#queryset-api)
   - **Methods that return `new queryset`**
   - all() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#all)
   - filter() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#filter)
   - annotate() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#annotate)
   - values() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#values)
   - values_list() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#values)
   - select_related() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#select-related)
   - prefetch_related() [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#prefetch-related)
   
   - **Methods that `don't return queryset`**
   - get()
   - create()
   - update()
   - delete()
   - aggregate()
   - **Query Related Tools `for complex query`**
   - Q() objects [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#q-objects)
   - F() objects [...](https://docs.djangoproject.com/en/4.0/ref/models/expressions/#django.db.models.F)


### Field Lookups [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#field-lookups)
   - **syntex** `<field_name>__<field_lookup>`
   - number `lt, lte, gt, gte, range`
   - charecter `startswith, istartswith, endswith, iendswith, exact, iexact`
   - date `date, year, month, day`
   - time `time, hour, munite, second`

### Aggregation Function [...](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#aggregation-functions)
   - Min()
   - Max()
   - Count()
   - Sum()
   - Avg()
