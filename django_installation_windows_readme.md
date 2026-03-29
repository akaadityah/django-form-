# Django Installation Guide for Windows 🐍

This guide explains how to install **Django on Windows** and create your
first Django project.

------------------------------------------------------------------------

## 📋 Prerequisites

Before installing Django, make sure you have:

-   Windows 10 or Windows 11
-   Internet connection
-   Python installed

Download Python from the official website:

https://www.python.org/downloads/

⚠️ While installing Python, make sure to enable:

✔ **Add Python to PATH**

------------------------------------------------------------------------

## 1️⃣ Check Python Installation

Open **Command Prompt** and run:

``` bash
python --version
```

or

``` bash
py --version
```

Example output:

    Python 3.x.x

------------------------------------------------------------------------

## 2️⃣ Install Django

Use **pip** (Python package manager) to install Django.

``` bash
pip install django
```

Wait for the installation to complete.

------------------------------------------------------------------------

## 3️⃣ Verify Django Installation

Run the following command:

``` bash
django-admin --version
```

Example output:

    5.x.x

This confirms Django is installed successfully.

------------------------------------------------------------------------

## 4️⃣ Create Your First Django Project

Navigate to the directory where you want to create the project:

``` bash
cd Desktop
```

Create a Django project:

``` bash
django-admin startproject myproject
```

Move into the project folder:

``` bash
cd myproject
```

------------------------------------------------------------------------

## 5️⃣ Run the Django Development Server

Start the server using:

``` bash
python manage.py runserver
```

Open your browser and visit:

    http://127.0.0.1:8000/

You should see the **Django welcome page**.

------------------------------------------------------------------------

## 6️⃣ Create a Django App

Inside the project directory, run:

``` bash
python manage.py startapp myapp
```

This will create a new Django application inside your project.

------------------------------------------------------------------------

## 📁 Project Structure

    myproject/
    │
    ├── manage.py
    ├── myproject/
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   ├── asgi.py
    │   └── wsgi.py
    │
    └── myapp/
        ├── admin.py
        ├── apps.py
        ├── models.py
        ├── views.py
        └── tests.py

------------------------------------------------------------------------

## ⭐ Recommended: Use Virtual Environment

Create a virtual environment:

``` bash
python -m venv venv
```

Activate it:

``` bash
venv\Scripts\activate
```

Install Django:

``` bash
pip install django
```

------------------------------------------------------------------------

## 🚀 Next Steps

After installing Django, you can start building projects such as:

-   Library Management System
-   Feedback System
-   Supermarket Billing System
-   Clinic Management System

------------------------------------------------------------------------

## 📚 Resources

Official Django Documentation:

https://docs.djangoproject.com/

------------------------------------------------------------------------

⭐ If you found this helpful, consider starring the repository!
