# Django Course 2024 - Complete Guide

This repository contains a comprehensive Django learning course with 10 progressive lessons and a final capstone project. Each lesson builds upon the previous one, introducing core Django concepts and best practices.

## Table of Contents

- [Lesson 1: Introduction to Django](#lesson-1-introduction-to-django)
- [Lesson 2: Django Setup and Configuration](#lesson-2-django-setup-and-configuration)
- [Lesson 3: Creating a Django App](#lesson-3-creating-a-django-app)
- [Lesson 4: Database Migration with SQLite3](#lesson-4-database-migration-with-sqlite3)
- [Lesson 5: SQLite Shell and iPython](#lesson-5-sqlite-shell-and-ipython)
- [Lesson 6: Rendering HTML Templates](#lesson-6-rendering-html-templates)
- [Lesson 7: Django Admin Dashboard](#lesson-7-django-admin-dashboard)
- [Lesson 8: Static Assets Management](#lesson-8-static-assets-management)
- [Lesson 9: Django Forms](#lesson-9-django-forms)
- [Lesson 10: User Authentication](#lesson-10-user-authentication)
- [Final Project: Inventory Management System](#final-project-inventory-management-system)

---

## Lesson 1: Introduction to Django

**Directory:** `lesson1-IntroToDjango/`

### Overview
This is the foundational lesson that introduces Django framework basics. It covers:

- **What is Django:** Understanding Django as a high-level Python web framework following the MTV (Model-Template-View) architecture
- **Django Project Structure:** Learning how Django organizes code into projects and apps
- **Creating a Django Project:** Using `django-admin startproject` to initialize a new project
- **URL Routing Basics:** Understanding how Django maps URLs to views using `urls.py`
- **Creating Views:** Building simple view functions to handle HTTP requests and return responses
- **Hello World Application:** Creating the simplest possible Django application to verify installation and setup

### Key Concepts
- Django's MTV architecture (Model-Template-View)
- Project vs. App structure
- URL routing and patterns
- View functions and HTTP requests/responses
- Django development server (`python manage.py runserver`)

### Project Structure
```
myproject/
├── manage.py
├── myapp/
│   ├── views.py
│   ├── urls.py
│   └── migrations/
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
```

---

## Lesson 2: Django Setup and Configuration

**Directory:** `lesson2-DjangoSetup/`

### Overview
This lesson dives deeper into Django's configuration and setup process. It teaches:

- **Settings Configuration:** Understanding `settings.py` and how to configure database, installed apps, middleware, and templates
- **Environment Variables:** Using environment variables to manage sensitive configuration data
- **Pipfile/Virtual Environment:** Setting up Python virtual environments using Pipenv for dependency management
- **Installation and Packages:** Installing Django and other required packages using pip or Pipenv
- **Django Settings Best Practices:** Organizing settings for different environments (development, testing, production)
- **Middleware:** Understanding Django middleware and how requests flow through the system

### Key Concepts
- Django settings structure (`INSTALLED_APPS`, `MIDDLEWARE`, `DATABASES`)
- Database configuration (SQLite, PostgreSQL, MySQL)
- Template directory configuration
- Static files and media configuration
- Secret key management
- Debug mode and allowed hosts
- Virtual environments and dependency management

### Skills Learned
- Creating and activating virtual environments
- Installing Django and dependencies
- Reading and modifying `settings.py`
- Understanding the request/response cycle

---

## Lesson 3: Creating a Django App

**Directory:** `lesson3-DjangoApp/`

### Overview
This lesson focuses on creating functional Django applications with database models. The example project is a "World Tour Agency" application that manages tours.

- **Creating Apps:** Using `python manage.py startapp` to generate app structure
- **Models:** Defining database models using Django's ORM (Object-Relational Mapping)
- **Model Fields:** Understanding different field types (CharField, TextField, IntegerField, ForeignKey, etc.)
- **Model Methods:** Adding custom methods to models like `__str__()`
- **Admin Registration:** Registering models in Django admin for easy management
- **App Configuration:** Configuring app-specific settings

### Key Concepts
- Model definition and field types
- Model relationships (ForeignKey, OneToOneField, ManyToManyField)
- Model meta options and model inheritance
- Django ORM basics
- Admin model registration

### Example Models
The lesson includes a `Tour` model with fields like name, description, price, duration, and destination.

---

## Lesson 4: Database Migration with SQLite3

**Directory:** `lesson4-MigrateSQLite3/`

### Overview
Database migrations are a critical part of Django development. This lesson covers:

- **What are Migrations:** Understanding database schema changes and version control
- **Creating Migrations:** Using `python manage.py makemigrations` to create migration files
- **Applying Migrations:** Using `python manage.py migrate` to apply changes to the database
- **Migration Files:** Understanding what's inside migration files and how Django tracks changes
- **Initial Data:** Loading initial data through migrations or fixtures
- **Rolling Back:** Reverting migrations when needed
- **Squashing Migrations:** Combining multiple migrations into one for cleaner history

### Key Concepts
- Django migration system
- Schema changes and version control
- Forward and backward migrations
- Custom migrations
- Data migrations

### Workflow
1. Modify models in `models.py`
2. Run `makemigrations` to create migration files
3. Run `migrate` to apply changes to database
4. Repeat as needed

---

## Lesson 5: SQLite Shell and iPython

**Directory:** `lesson5-SQLiteShell-iPython/`

### Overview
This lesson teaches database interaction and querying techniques:

- **SQLite Command Line:** Using sqlite3 shell to directly query the database
- **Django Shell:** Using `python manage.py shell` for interactive Django environment
- **iPython Integration:** Enhanced interactive shell with better syntax highlighting and introspection
- **Querying Data:** Using Django ORM to fetch, filter, and manipulate data
- **Database Analysis:** Directly examining database schema and data
- **Testing Queries:** Verifying that models work correctly before using them in views

### Key Concepts
- Django shell and ORM queries
- QuerySet operations
- Database introspection
- iPython features (tab completion, magic commands)
- Data validation and testing

### Common Queries
```python
Tour.objects.all()  # Get all tours
Tour.objects.filter(price__lt=100)  # Filter tours by price
Tour.objects.get(id=1)  # Get specific tour
Tour.objects.create(name="New Tour", price=150)  # Create new tour
```

---

## Lesson 6: Rendering HTML Templates

**Directory:** `lesson6-RenderHTMLTemplate/`

### Overview
Templates are essential for displaying data to users. This lesson covers:

- **Template Structure:** Creating HTML templates that Django can render
- **Template Tags:** Using Django template tags like `{% for %}`, `{% if %}`, `{% block %}`
- **Template Filters:** Applying filters to variables for formatting (e.g., `{{ date|date:"Y-m-d" }}`)
- **Template Inheritance:** Using base templates to DRY up HTML code
- **Template Context:** Passing data from views to templates
- **Static Template Rendering:** Understanding how Django finds and renders templates
- **Template Directory Configuration:** Setting up `TEMPLATES` in `settings.py`

### Key Concepts
- Template syntax and variables
- Template tags and filters
- Template inheritance (extends, blocks)
- Template context passing
- Rendering templates with `render()`
- Template loaders

### Example View
```python
def index(request):
    tours = Tour.objects.all()
    context = {'tours': tours}
    return render(request, 'tours/index.html', context)
```

### Example Template
```html
{% extends 'base.html' %}
{% block content %}
    <h1>Available Tours</h1>
    {% for tour in tours %}
        <div class="tour">
            <h2>{{ tour.name }}</h2>
            <p>Price: ${{ tour.price }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

---

## Lesson 7: Django Admin Dashboard

**Directory:** `lesson7-AdminDashboard/`

### Overview
Django's built-in admin interface is powerful for managing application data. This lesson teaches:

- **Admin Registration:** Registering models to make them manageable via admin
- **Admin Customization:** Customizing the admin interface with `ModelAdmin` class
- **List Display:** Configuring which fields appear in the model list view
- **Search and Filtering:** Adding search fields and list filters
- **Admin Actions:** Creating custom admin actions for bulk operations
- **Permissions:** Understanding and managing admin permissions
- **Admin Templates:** Customizing admin interface appearance
- **Raw ID Fields:** Handling foreign key relationships in admin

### Key Concepts
- `admin.site.register()`
- `ModelAdmin` class
- `list_display`, `list_filter`, `search_fields`
- Custom admin actions
- User permissions and groups
- Admin authentication

### Example Admin Configuration
```python
from django.contrib import admin
from .models import Tour

class TourAdmin(admin.ModelAdmin):
    list_display = ['name', 'price', 'duration']
    search_fields = ['name', 'destination']
    list_filter = ['price', 'duration']

admin.site.register(Tour, TourAdmin)
```

---

## Lesson 8: Static Assets Management

**Directory:** `lesson8-StaticAssets/`

### Overview
Static files (CSS, JavaScript, images) require proper management in Django. This lesson covers:

- **Static Files Configuration:** Setting up `STATIC_URL` and `STATIC_ROOT` in settings
- **Serving Static Files:** How Django serves CSS, JavaScript, and images
- **Static Files in Templates:** Using `{% static %}` template tag
- **Static File Finders:** Understanding how Django locates static files
- **Collecting Static Files:** Using `python manage.py collectstatic` for production
- **Media Files:** Handling user-uploaded files (separate from static files)
- **Development vs. Production:** Different static file handling in development and production
- **Static File Organization:** Best practices for organizing CSS, JS, and images

### Key Concepts
- Static file configuration
- `{% static %}` template tag
- `python manage.py collectstatic`
- Static file finders
- Media files and user uploads
- CDN integration for static files

### Directory Structure
```
app/
├── static/
│   ├── css/
│   ├── js/
│   └── images/
├── templates/
├── media/  (for user uploads)
```

---

## Lesson 9: Django Forms

**Directory:** `lesson9-DjangoForms/`

### Overview
Forms are crucial for user input handling. This lesson teaches form creation and validation:

- **Django Forms:** Creating forms using `django.forms.Form` class
- **Model Forms:** Using `ModelForm` to automatically generate forms from models
- **Form Fields:** Understanding different field types (CharField, EmailField, IntegerField, etc.)
- **Form Widgets:** Customizing form input widgets (TextInput, Select, CheckboxInput, etc.)
- **Form Validation:** Client-side and server-side validation
- **Form Errors:** Displaying and handling form errors
- **Form Processing:** Processing form submissions in views
- **CSRF Protection:** Understanding Django's CSRF token for security
- **Form Rendering:** Different ways to render forms in templates

### Key Concepts
- `Form` and `ModelForm` classes
- Form fields and widgets
- Form validation (`clean_*` methods, `clean()`)
- CSRF tokens
- Form processing in views
- Form rendering in templates

### Example Form
```python
from django import forms

class TourForm(forms.ModelForm):
    class Meta:
        model = Tour
        fields = ['name', 'price', 'duration', 'destination']
```

### Form Processing
```python
def create_tour(request):
    if request.method == 'POST':
        form = TourForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('tour_list')
    else:
        form = TourForm()
    return render(request, 'create_tour.html', {'form': form})
```

---

## Lesson 10: User Authentication

**Directory:** `lesson10-Authentication/`

### Overview
User authentication and authorization are fundamental to web applications. This lesson covers:

- **Django Authentication System:** Built-in user authentication
- **User Model:** Understanding Django's `User` model
- **Password Hashing:** How Django securely stores passwords
- **Authentication Functions:** Using `authenticate()`, `login()`, `logout()`
- **User Registration:** Creating user registration systems
- **Login and Logout:** Implementing login and logout functionality
- **Login Required Decorator:** Protecting views with `@login_required`
- **Class-Based View Protection:** Using `LoginRequiredMixin` for class-based views
- **Permissions and Groups:** Managing user permissions and roles
- **Custom User Model:** Extending the default `User` model
- **Session Management:** Understanding Django sessions

### Key Concepts
- Django's `User` model
- Password hashing and verification
- `authenticate()`, `login()`, `logout()`
- `@login_required` decorator
- `LoginRequiredMixin` for CBVs
- User permissions and groups
- Session management
- Custom authentication backends

### Example Authentication Views
```python
def register_view(request):
    if request.method == "POST":
        form = RegisterForm(request.POST)
        if form.is_valid():
            username = form.cleaned_data.get("username")
            password = form.cleaned_data.get("password")
            user = User.objects.create_user(username=username, password=password)
            login(request, user)
            return redirect('home')
    else:
        form = RegisterForm()
    return render(request, 'register.html', {'form': form})

@login_required
def home_view(request):
    return render(request, 'home.html')
```

---

## Final Project: Inventory Management System

**Directory:** `FinalProject/`

### Overview
The final project brings together all lessons to create a complete web application for managing an inventory system. This is a practical, real-world application demonstrating professional Django development practices.

### Application Features

#### 1. **Product Management**
- Create, Read, Update, and Delete (CRUD) operations for products
- Product fields: Product ID, Name, SKU, Price, Quantity, Supplier
- Database persistence with SQLite3

#### 2. **User Authentication**
- User registration and login system
- Secure password handling
- Session management
- Logout functionality
- Protected views accessible only to authenticated users

#### 3. **Admin Dashboard**
- Django admin interface for administrators
- Managing products, users, and permissions
- Admin-only operations for data management

#### 4. **Product Database**
- SQLite database for storing inventory
- Proper migrations for schema management
- Data validation and constraints

#### 5. **User Interface**
- HTML templates for displaying products
- Template inheritance for consistent styling
- Forms for product creation and updating
- User-friendly dashboard

#### 6. **Search and Filtering**
- Search products by name or SKU
- Filter products by price range
- Sort products by different criteria

### Project Structure
```
FinalProject/
├── Pipfile
├── invProject/  (Project folder)
│   ├── manage.py
│   ├── db.sqlite3
│   ├── invProject/  (Project settings)
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── wsgi.py
│   │   └── asgi.py
│   └── invApp/  (Main application)
│       ├── models.py (Product model)
│       ├── views.py (CRUD views)
│       ├── urls.py (URL routing)
│       ├── forms.py (Product forms)
│       ├── admin.py (Admin configuration)
│       ├── templates/  (HTML templates)
│       ├── static/  (CSS, JS, images)
│       └── migrations/  (Database migrations)
```

### Key Models

#### Product Model
```python
class Product(models.Model):
    product_id = models.AutoField(primary_key=True)
    name = models.CharField(max_length=100)
    sku = models.CharField(max_length=50, unique=True)
    price = models.FloatField()
    quantity = models.IntegerField()
    supplier = models.CharField(max_length=100)
    
    def __str__(self):
        return self.name
```

### Core Functionality

1. **List Products:** Display all products in inventory with pagination
2. **Add Product:** Form to add new products to inventory
3. **Edit Product:** Update existing product information
4. **Delete Product:** Remove products from inventory
5. **Search:** Search products by name or SKU
6. **User Dashboard:** Personal dashboard for logged-in users

### Running the Project

```bash
cd FinalProject/invProject
python manage.py runserver
```

Visit `http://localhost:8000/` in your browser.

### Admin Access

```bash
python manage.py createsuperuser
```

Then visit `http://localhost:8000/admin/` with your superuser credentials.

### Technologies Used
- **Framework:** Django 3.x/4.x
- **Database:** SQLite3
- **Frontend:** HTML5, CSS3, Bootstrap (optional)
- **Python:** 3.8+

---

## Course Learning Outcomes

Upon completing this course, you will understand:

✅ Django project and app structure  
✅ Models, Views, and Templates (MTV architecture)  
✅ Database models and migrations  
✅ HTML template rendering and inheritance  
✅ Django's powerful admin interface  
✅ User authentication and authorization  
✅ Form handling and validation  
✅ Static files and media management  
✅ URL routing and configuration  
✅ Building complete web applications  

---

## Getting Started

### Prerequisites
- Python 3.8 or higher
- pip or pipenv for package management
- Basic understanding of Python

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd django_course_2024
```

2. Navigate to any lesson directory:
```bash
cd lesson1-IntroToDjango
```

3. Create and activate virtual environment:
```bash
pipenv install
pipenv shell
```

4. Run migrations:
```bash
python myproject/manage.py migrate
```

5. Start the development server:
```bash
python myproject/manage.py runserver
```

---

## Tips for Success

1. **Complete Lessons Sequentially:** Each lesson builds on previous knowledge
2. **Experiment:** Modify code and see what happens
3. **Use Django Shell:** Practice ORM queries in the Django shell
4. **Read the Code:** Understand the structure of each component
5. **Build Incrementally:** Add features step by step
6. **Reference Django Docs:** The official Django documentation is excellent
7. **Practice CRUD:** Ensure you understand Create, Read, Update, Delete operations

---

## Additional Resources

- [Official Django Documentation](https://docs.djangoproject.com/)
- [Django for Beginners](https://djangoforbeginners.com/)
- [Real Python Django Tutorials](https://realpython.com/django/)
- [Django Girls Tutorial](https://tutorial.djangogirls.org/)

---

**Happy Learning! 🚀**
