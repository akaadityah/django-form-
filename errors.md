# 🛠️ Django Common Errors & Fixes

This section covers **10 common Django errors beginners face** and how to fix them.

These solutions solve **about 90% of beginner Django problems**.

---

# 1️⃣ Port Already in Use

### ❌ Error

```
Error: That port is already in use
```

### ✅ Fix

Run server on another port:

```bash
python3 manage.py runserver 8001
```

Or kill the running process:

```bash
sudo lsof -i :8000
sudo kill -9 PID
```

---

# 2️⃣ Unapplied Migrations

### ❌ Error

```
You have unapplied migrations
```

### ✅ Fix

Run migrations:

```bash
python3 manage.py migrate
```

---

# 3️⃣ ModuleNotFoundError

### ❌ Error

```
ModuleNotFoundError: No module named 'django'
```

### ✅ Fix

Install Django:

```bash
pip3 install django
```

Or activate your virtual environment before running the project.

---

# 4️⃣ TemplateDoesNotExist

### ❌ Error

```
TemplateDoesNotExist: accounts/login.html
```

### ⚠️ Cause

Template folder structure is incorrect or missing.

### ✅ Fix Folder Structure

```
accounts
 └── templates
      └── accounts
           └── login.html
```

---

# 5️⃣ 404 Page Not Found

### ❌ Error

```
Page not found (404)
```

### ⚠️ Cause

URL is not defined in `urls.py`.

### ✅ Fix

Add route in `urls.py`:

```python
path('login/', views.login_view)
```

---

# 6️⃣ Database Table Not Found

### ❌ Error

```
no such table: auth_user
```

### ✅ Fix

Run migrations:

```bash
python3 manage.py migrate
```

---

# 7️⃣ App Not Installed

### ❌ Error

```
No installed app with label 'accounts'
```

### ✅ Fix

Add the app inside **settings.py**

```python
INSTALLED_APPS = [
    'accounts',
]
```

---

# 8️⃣ Static Files Not Loading

### ❌ Error

CSS or JS files are not loading.

### ✅ Fix

Add in `settings.py`:

```python
STATIC_URL = 'static/'
```

Then run:

```bash
python3 manage.py collectstatic
```

---

# 9️⃣ Permission Denied (Ubuntu)

### ❌ Error

```
Permission denied
```

### ✅ Fix

Give execute permission:

```bash
chmod +x manage.py
```

---

# 🔟 Server Not Starting

### ❌ Error

```
python: command not found
```

### ✅ Fix

Use Python3:

```bash
python3 manage.py runserver
```

---

# 💡 Tip

These **10 issues cover about 90% of Django beginner errors**.

If you face a problem, check these fixes first.

---

⭐ Happy Coding with Django!
