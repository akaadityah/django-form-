# 📩 Django Contact Form Setup Guide (Ubuntu)

This guide explains how to create and run a simple **Contact Form** (Name, Email, Description) using Django on Ubuntu.

---

## 📌 Prerequisites

* Python 3
* pip
* Django

Install Django:

```bash
pip install django
```

---

## 🚀 1️⃣ Create Django Project

```bash
django-admin startproject myproject
cd myproject
```

---

## 📦 2️⃣ Create App

```bash
python3 manage.py startapp contact
```

---

## ⚙️ 3️⃣ Register App

Open:

```
myproject/settings.py
```

Add inside `INSTALLED_APPS`:

```python
'contact',
```

---

## 📁 4️⃣ Create Template Folder

```bash
mkdir -p contact/templates
touch contact/templates/contact.html
```

---

## 📝 5️⃣ Add HTML Form

Paste inside `contact/templates/contact.html`:

```html
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
```

---

## 🧠 6️⃣ Create View

Open:

```
contact/views.py
```

Replace with:

```python
from django.shortcuts import render

def contact_view(request):
    if request.method == "POST":
        name = request.POST.get("name")
        email = request.POST.get("email")
        description = request.POST.get("description")

        print(name, email, description)

    return render(request, "contact.html")
```

---

## 🔗 7️⃣ Create App URLs

Create:

```
contact/urls.py
```

Add:

```python
from django.urls import path
from .views import contact_view

urlpatterns = [
    path('', contact_view, name='contact'),
]
```

---

## 🌐 8️⃣ Connect URLs to Project

Open:

```
myproject/urls.py
```

Update:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('contact/', include('contact.urls')),
]
```

---

## ▶️ 9️⃣ Run Server

```bash
python3 manage.py runserver
```

Open browser:

```
http://127.0.0.1:8000/contact/
```

---

## ✅ Result

You now have a working Django Contact Form.
Submitted data will be printed in the terminal.

---

## 🔮 Future Improvements

* Save data to database
* Add success message
* Add form validation
* Use Django Forms
* Add Bootstrap styling

---


⭐ Happy Coding!
