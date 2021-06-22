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
