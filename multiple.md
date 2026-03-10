# 🔐 Django Multi-Page Login System Guide (Ubuntu)

This guide explains how to create a **Login System with multiple pages** using Django.

### 📄 Pages Included

```
Login Page → Dashboard → Logout
           → Error Page
```

---

# 📌 Prerequisites

Install Django:

```bash
pip install django
```

Check version:

```bash
django-admin --version
```

---

# 🚀 1️⃣ Create Django Project

```bash
django-admin startproject myproject
cd myproject
```

### Project Structure

```
myproject/
 ├── manage.py
 └── myproject/
     ├── __init__.py
     ├── settings.py
     ├── urls.py
     ├── asgi.py
     └── wsgi.py
```

---

# 📦 2️⃣ Create App

```bash
python3 manage.py startapp accounts
```

### App Structure

```
accounts/
 ├── admin.py
 ├── apps.py
 ├── models.py
 ├── views.py
 ├── tests.py
 └── migrations/
```

---

# ⚙️ 3️⃣ Register App

Open:

```
myproject/settings.py
```

Add inside `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'accounts',
]
```

---

# 🗄️ 4️⃣ Run Database Migrations

Django authentication requires database tables.

Run:

```bash
python manage.py migrate
```

Database file created:

```
db.sqlite3
```

---

# 📁 5️⃣ Create Template Folder

Create template directory:

```bash
mkdir -p accounts/templates/accounts
```

Create these files:

```
login.html
dashboard.html
error.html
```

---

# 📝 6️⃣ Login Page

File:

```
accounts/templates/accounts/login.html
```

```html
<!DOCTYPE html>
<html>
<head>
<title>Login</title>
</head>

<body>

<h2>Login Page</h2>

<form method="post">
{% csrf_token %}

<label>Username</label><br>
<input type="text" name="username"><br><br>

<label>Password</label><br>
<input type="password" name="password"><br><br>

<button type="submit">Login</button>

</form>

</body>
</html>
```

---

# 📝 7️⃣ Dashboard Page

File:

```
accounts/templates/accounts/dashboard.html
```

```html
<!DOCTYPE html>
<html>
<body>

<h2>Welcome to Dashboard</h2>

<p>You are logged in successfully!</p>

<a href="/logout/">Logout</a>

</body>
</html>
```

---

# 📝 8️⃣ Error Page

File:

```
accounts/templates/accounts/error.html
```

```html
<!DOCTYPE html>
<html>
<body>

<h2>Login Failed</h2>

<p>Invalid username or password</p>

<a href="/login/">Try Again</a>

</body>
</html>
```

---

# 🧠 9️⃣ Create Views

Open:

```
accounts/views.py
```

Add:

```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout

def login_view(request):

    if request.method == "POST":

        username = request.POST.get("username")
        password = request.POST.get("password")

        user = authenticate(request, username=username, password=password)

        if user is not None:
            login(request, user)
            return redirect("dashboard")
        else:
            return redirect("error")

    return render(request, "accounts/login.html")


def dashboard(request):

    if request.user.is_authenticated:
        return render(request, "accounts/dashboard.html")
    else:
        return redirect("login")


def logout_view(request):

    logout(request)
    return redirect("login")


def error_page(request):

    return render(request, "accounts/error.html")
```

---

# 🔗 🔟 Create URLs

Create file:

```
accounts/urls.py
```

Add:

```python
from django.urls import path
from . import views

urlpatterns = [

path('login/', views.login_view, name='login'),
path('dashboard/', views.dashboard, name='dashboard'),
path('logout/', views.logout_view, name='logout'),
path('error/', views.error_page, name='error'),

]
```

---

# 🌐 1️⃣1️⃣ Connect Project URLs

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
path('', include('accounts.urls')),

]
```

---

# 👤 1️⃣2️⃣ Create Superuser

Create a login account:

```bash
python manage.py createsuperuser
```

Enter:

```
Username
Email
Password
```

---

# ▶️ 1️⃣3️⃣ Run Server

```bash
python manage.py runserver
```

Open in browser:

```
http://127.0.0.1:8000/login/
```

---

# ✅ Result

You now have a working **Django Multi-Page Login System** with:

* Login Page
* Dashboard Page
* Logout System
* Error Page

---

⭐ Happy Coding with Django!
