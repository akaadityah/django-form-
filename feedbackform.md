# 📝 Django Feedback System (Name, Rating, Comment)

This project demonstrates a **simple Django Feedback System** where users can submit:

* 👤 Name
* ⭐ Rating
* 💬 Comment

After submitting the form, the entered feedback is displayed on a **success page**.

---

# 📌 Prerequisites

Make sure the following are installed:

* Python 3
* pip
* Django

Install Django:

```bash
pip install django
```

Check installation:

```bash
django-admin --version
```

---

# 🚀 1️⃣ Create Django Project

```bash
django-admin startproject feedbackproject
```

Move into the project directory:

```bash
cd feedbackproject
```

---

# 📦 2️⃣ Create App

```bash
python manage.py startapp feedbackapp
```

### Project Structure

```
feedbackproject
│
├── feedbackproject
│   └── settings.py
│
├── feedbackapp
│   ├── models.py
│   ├── views.py
│   ├── forms.py
│
└── manage.py
```

---

# ⚙️ 3️⃣ Register App

Open:

```
feedbackproject/settings.py
```

Add the app inside `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
'django.contrib.admin',
'django.contrib.auth',
'feedbackapp',
]
```

---

# 🗄️ 4️⃣ Create Model

Open:

```
feedbackapp/models.py
```

Add the following code:

```python
from django.db import models

class Feedback(models.Model):
    name = models.CharField(max_length=100)
    rating = models.IntegerField()
    comment = models.TextField()

    def __str__(self):
        return self.name
```

---

# 🗄️ 5️⃣ Run Database Migration

```bash
python manage.py makemigrations
python manage.py migrate
```

This will create the **SQLite database**.

---

# 📋 6️⃣ Create forms.py

Create file:

```
feedbackapp/forms.py
```

Add:

```python
from django import forms
from .models import Feedback

class NameForm(forms.ModelForm):
    class Meta:
        model = Feedback
        fields = ['name']

class RatingForm(forms.ModelForm):
    class Meta:
        model = Feedback
        fields = ['rating']

class CommentForm(forms.ModelForm):
    class Meta:
        model = Feedback
        fields = ['comment']
```

---

# 🧠 7️⃣ Create Views

Open:

```
feedbackapp/views.py
```

Add:

```python
from django.shortcuts import render, redirect
from .forms import NameForm, RatingForm, CommentForm
from .models import Feedback

def feedback_view(request):

    form1 = NameForm()
    form2 = RatingForm()
    form3 = CommentForm()

    if request.method == "POST":
        form1 = NameForm(request.POST)
        form2 = RatingForm(request.POST)
        form3 = CommentForm(request.POST)

        if form1.is_valid() and form2.is_valid() and form3.is_valid():

            feedback = form1.save(commit=False)
            feedback.rating = form2.cleaned_data['rating']
            feedback.comment = form3.cleaned_data['comment']
            feedback.save()

            return redirect('success', id=feedback.id)

    return render(request,'feedback.html',{'form1':form1,'form2':form2,'form3':form3})


def success(request,id):

    feedback = Feedback.objects.get(id=id)

    return render(request,'success.html',{'feedback':feedback})
```

---

# 🔗 8️⃣ Create URLs

## feedbackapp/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
path('',views.feedback_view,name='feedback'),
path('success/<int:id>/',views.success,name='success')
]
```

---

## feedbackproject/urls.py

```python
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
path('admin/',admin.site.urls),
path('',include('feedbackapp.urls')),
]
```

---

# 📄 9️⃣ Create Templates

Create folder:

```
feedbackapp/templates
```

---

## feedback.html

```html
<h2>Feedback Form</h2>

<form method="POST">

{% csrf_token %}

<p>Name</p>
{{ form1 }}

<p>Rating</p>
{{ form2 }}

<p>Comment</p>
{{ form3 }}

<button type="submit">Submit</button>

</form>
```

---

## success.html

```html
<h2>Thank You For Your Feedback</h2>

<p>Name: {{ feedback.name }}</p>

<p>Rating: {{ feedback.rating }}</p>

<p>Comment: {{ feedback.comment }}</p>

<a href="/">Give Another Feedback</a>
```

---

# ▶️ 1️⃣0️⃣ Run Server

```bash
python manage.py runserver
```

Open browser:

```
http://127.0.0.1:8000
```

---

# ✅ Output

### Page 1

```
Feedback Form
Name
Rating
Comment
Submit
```

### Page 2

```
Thank You For Your Feedback
Name: Aditya
Rating: 5
Comment: Good Website
```

---

# 🚀 Future Improvements

* Save feedback to admin panel
* Add Bootstrap styling
* Add rating stars ⭐
* Show feedback list page
* Add validation

---

⭐ Simple Django Project for Beginners.
