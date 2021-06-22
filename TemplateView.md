> **Arguments**

+ template_name = None
+ template_engine = None
+ response_class = TemplateResponse
+ content_type = None
+ extra_context = None
    
    
> **Method**
```
    def render_to_response(self, context, **response_kwargs):
        """
        Return a response, using the `response_class` for this view, with a
        template rendered with the given context.

        Pass response_kwargs to the constructor of the response class.
        """
```

```
    def get_template_names(self):
        """
        Return a list of template names to be used for the request. Must return
        a list. May not be called if render_to_response() is overridden.
        """
```

```
    def get_context_data(self, **kwargs):
```

---

> **Pass TemplateView with url**
> 
> *urls.py*

```
app_name = 'classapp'
urlpatterns = [
    path('', views.TemplateView.as_view(template_name='classapp/dashboard.html'), name='dashboard'),
```

---

> **TemplateView using *views.py***

**urls.py**
```
from django.urls import path
from . import views


app_name = 'classapp'
urlpatterns = [
    path('dashboard/', views.DashboardView.as_view(), name='dashboard'),
    # If you want to use extra context then comment the first one and remove comment the second path.
    # path('dashboard/', views.DashboardView.as_view(extra_context={'course': 'Python'}, name='dashboard'),
    
```
**views.py**
```
from django.views.generic.base import TemplateView


class DahsboardView(TemplateView):
    template_name = 'classapp/dashboard.html'

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        
        # context['name'] = 'Apt Yam'
        # context['roll'] = 101

        context = {'name': 'Apt Yam', 'roll': '101'}
        return context
```
