 ## Registration Form(views.py)
 ```
  from django.shortcuts import render, redirect
 from django.contrib.auth import login
 from django.contrib import messages
 from django.contrib.auth.forms import authenticate
 
 
 def registration_view(request):
    if not request.user.is_authenticated:
        if request.method == "POST":
            form = UserRegForm(request.POST)
            if form.is_valid():
                form.save()
                new_user = authenticate(username=form.cleaned_data['username'],
                                        password=form.cleaned_data['password1'])
                login(request, new_user)
                messages.add_message(request, messages.INFO, f'{request.user} registered successfully.')
                return redirect('/')
        else:
            form = UserRegForm()
        return render(request, 'forms/registration.html', {'form': form})
    else:
        return redirect('/')
 ```
 
  ## Login Form(views.py)
 ```
 from django.shortcuts import render, redirect
 from django.contrib.auth import login
 from django.contrib import messages
 from django.contrib.auth.forms import authenticate, AuthenticationForm
 
 
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
                    messages.add_message(request, messages.SUCCESS, f'{request.user} logged in successfully.')
                    return redirect('/dashboard/')
        else:
            form = AuthenticationForm()
        return render(request, 'forms/login.html', {'form': form})
    else:
        return redirect('/')
 ```
 
## Logout Form(views.py)
```
from django.contrib.auth import logout
from django.shortcuts import render, redirect
from django.contrib import messages


def logout_view(request):
    if request.user.is_authenticated:
        messages.add_message(request, messages.SUCCESS, f'{request.user} logout successfully.')
        logout(request)
        return redirect('/login/')
    else:
        return redirect('/login/')
```

## Change Password(views.py)
```
from django.shortcuts import render, redirect
from django.contrib.auth.forms import PasswordChangeForm
from django.contrib.auth import update_session_auth_hash
from django.contrib import messages


def changed_password(request):
    if request.user.is_authenticated:
        if request.method == "POST":
            form = PasswordChangeForm(user=request.user, data=request.POST)
            if form.is_valid():
                form.save()
                update_session_auth_hash(request, user=form.user)
                return redirect('/')
        else:
            form = PasswordChangeForm(user=request.user)
        return render(request, 'forms/password_changed.html', {'form': form})
    else:
        return redirect('/login/')
```

## User Profile or Dashboard(views.py)
> forms.py

```
from django import forms
from django.contrib.auth.forms import UserChangeForm


class UserDashboardForm(UserChangeForm):
    date_joined = forms.DateTimeField(disabled=True)
    last_login = forms.DateTimeField(disabled=True)

    class Meta:
        model = User
        fields = ['username', 'first_name', 'last_name', 'email', 'date_joined', 'last_login']
        
```

> views.py
```
def dashboard(request):
    if request.user.is_authenticated:
        if request.method == "POST":
            form = EditDashboard(request.POST, instance=request.user)
            if form.is_valid():
                form.save()
        else:
            form = EditDashboard(instance=request.user)
        return render(request, 'forms/dashboard.html', {'form': form, 'name': request.user})
    else:
        return HttpResponseRedirect('/login/')
```
