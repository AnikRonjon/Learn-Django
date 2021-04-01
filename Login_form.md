 ## Registration Form(views.py
 ```
 def registration_view(request):
    if not request.user.is_authenticated:
        if request.method == "POST":
            form = UserRegForm(request.POST)
            if form.is_valid():
                messages.add_message(request, messages.INFO, 'You loge in successfully.')
                new_user = form.save()
                new_user = authenticate(username=form.cleaned_data['username'],
                                        password=form.cleaned_data['password1'])
                login(request, new_user)
                return HttpResponseRedirect('/')
        else:
            form = UserRegForm()
        return render(request, 'forms/registration.html', {'form': form})
    else:
        return HttpResponseRedirect('/')
 ```
 
  ## Login Form(views.py)
 ```
 def login_view(request):
    if not request.user.is_authenticated:
        if request.method == "POST":
            form = AuthenticationForm(request=request, data=request.POST)
            if form.is_valid():
                name = form.cleaned_data['username']
                passwd = form.cleaned_data['password']
                user = authenticate(username=name, password=passwd)
                if user is not None:
                    login(request, user)
                    messages.add_message(request, messages.INFO, 'You logged in successfully.')
                    return HttpResponseRedirect('/dashboard/')
        else:
            form = AuthenticationForm()
        return render(request, 'forms/login.html', {'form': form, 'name': request.user})
    else:
        return HttpResponseRedirect('/')
 ```
 
## Logout Form(views.py)
```
def logout_view(request):
    if request.user.is_authenticated:
        logout(request)
        return HttpResponseRedirect('/')
    else:
        return HttpResponseRedirect('/login/')
```
