# Hands-On 2: Django Web App 🌐

This hands-on project demonstrates how to create and run a basic Django web application locally using **Windows OS**, and later containerize it using Docker.

## 🛠️ Project Setup on Windows

### ✅ Step 1: Create Project Directory

```bash
mkdir demo-webapp
cd demo-webapp
````

### ✅ Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

> This will create a `venv/` folder to manage dependencies locally.

### ✅ Step 3: Activate Virtual Environment

```bash
.\venv\Scripts\activate
```

### ✅ Step 4: Install Django

```bash
python -m pip install Django
```


## 🚀 Start the First Django Project

### ✅ Step 1: Create Django Project

```bash
django-admin startproject demoApp .
```

### ✅ Step 2: Run the Development Server

```bash
python manage.py runserver
```

> Visit: [http://localhost:8000](http://localhost:8000)
> You should see the Django welcome page.

## 📦 Add the Pages App

### ✅ Step 1: Create the App

```bash
python manage.py startapp pages
```

### ✅ Step 2: Register the App in `settings.py`

In `demoApp/settings.py`, add the app config to `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    "pages.apps.PagesConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

## 🎨 Create a View and Template

### ✅ Step 1: Define a View

In `pages/views.py`, add:

```python
from django.shortcuts import render

def home(request):
    return render(request, "pages/home.html", {})
```

### ✅ Step 2: Create Templates

Create this folder structure:

```
demo-webapp/
└── pages/
    └── templates/
        └── pages/
            └── home.html
```

Inside `home.html`, write:

```html
<h1>Hello, World!</h1>
```

## 🌐 URL Routing

### ✅ Step 1: Update Main URL Configuration

In `demoApp/urls.py`, modify to include the pages app:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("pages.urls")),
]
```

### ✅ Step 2: Create `pages/urls.py`

Create a new file `pages/urls.py` and add:

```python
from django.urls import path
from pages import views

urlpatterns = [
    path("", views.home, name="home"),
]
```

## ✅ Run the Server Again

If the development server isn't running:

```bash
python manage.py runserver
```

Now open your browser at:
👉 [http://localhost:8000](http://localhost:8000)
You should see the “Hello, World!” page rendered via Django.

## 🐳 Dockerizing the Django App

At first, I created a Dockerfile using Ubuntu as the base image. But the line:

```dockerfile
pip install -r requirements.txt
```

did not work because **Ubuntu 24.04 introduced PEP 668**, which prevents pip from modifying the system Python environment directly. To temporarily fix it, I used:

```dockerfile
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install --break-system-packages -r requirements.txt
```

> ⚠️ Not ideal for production, but works in local container builds.

### ✅ Recommended: Use Python Base Image Instead

So I switched to the official Python base image, and the final working `Dockerfile` is:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt /app/
COPY demo-webapp /app/demo-webapp

RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /app/demo-webapp

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
```

### 🏗️ Build the Docker Image

```bash
docker build -t django-demo-app .
```

* `-t django-demo-app`: tags the image with a name
* `.`: uses the current directory containing Dockerfile and app

Alternatively, you can build without a tag:

```bash
docker build .
```

List all images:

```bash
docker images
```

### ▶️ Run the Container

```bash
docker run -p 8000:8000 django-demo-app
```

This maps **host port 8000** to **container port 8000**, so you can access your Django app at:
👉 [http://localhost:8000](http://localhost:8000)


## 📚 Resources

* [Understand the Structure of a Django Website – Real Python](https://realpython.com/get-started-with-django-1/#understand-the-structure-of-a-django-website)
* [Django Docker Tutorial Video (YouTube)](https://youtu.be/3IAvr_O6vao?si=Zyi-eJMYEOZ3afMI)

