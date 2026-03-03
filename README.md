# Django Contact Form Setup Guide (Ubuntu)

This guide explains how to create and run a simple Contact Form
(Name, Email, Description) using Django on Ubuntu.

---

## 1️⃣ Install Python and Django

Open Terminal:

django-admin startproject myproject
cd myproject

2️⃣ Create Django Project

django-admin startproject myproject
cd myproject

3️⃣ Create App
python3 manage.py startapp contact

Step 4: Register App

Open settings file:
myproject/settings.py

Add inside INSTALLED_APPS:

'contact',

5️⃣ Create Template Folder
mkdir contact/templates
contact/templates/contact.html


Paste this inside contact.html:

<!DOCTYPE html>
<html>
<head>
    <title>Contact Form</title>
</head>
<body>

<h2>Contact Form</h2>

<form method="post">
    {% csrf_token %}

    <label>Name:</label><br>
    <input type="text" name="name"><br><br>

    <label>Email:</label><br>
    <input type="email" name="email"><br><br>

    <label>Description:</label><br>
    <textarea name="description"></textarea><br><br>

    <button type="submit">Submit</button>
</form>

</body>
</html>

6️⃣ Create View

Open:
contact/views.py

Replace with:

from django.shortcuts import render

def contact_view(request):
    if request.method == "POST":
        name = request.POST.get("name")
        email = request.POST.get("email")
        description = request.POST.get("description")

        print(name, email, description)

    return render(request, "contact.html")


7️⃣ Create App URLs
contact/urls.py

Add:

from django.urls import path
from .views import contact_view

urlpatterns = [
    path('', contact_view, name='contact'),
]

8️⃣ Connect URLs to Project

Open:

nano myproject/urls.py

Update file:

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('contact/', include('contact.urls')),
]

9️⃣ Run Server
python3 manage.py runserver

Open browser:

http://127.0.0.1:8000/contact/



