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
 
