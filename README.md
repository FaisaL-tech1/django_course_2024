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

### Code Examples

#### Creating Views (myapp/views.py)
The view is a Python function that receives a web request and returns a web response:

```python
from django.shortcuts import render
from django.http import HttpResponse

# Simple view that returns plain text
def hello_world(request):
    return HttpResponse("Hello, World! Welcome to Django.")

# View that receives URL parameters
def greet_user(request, name):
    return HttpResponse(f"Hello, {name}!")
```

#### URL Routing (myapp/urls.py)
Maps URLs to view functions using URL patterns:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.hello_world, name='hello'),
    path('greet/<str:name>/', views.greet_user, name='greet'),
]
```

#### Project URL Configuration (myproject/urls.py)
The main project URL file includes app URLs:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),  # Include app URLs
]
```

### Request/Response Cycle
1. User visits a URL: `http://localhost:8000/hello/`
2. Django matches URL to pattern in `urls.py`
3. View function is called with the request object
4. View returns an `HttpResponse`
5. Response is sent back to the browser

### Running the Application
```bash
python manage.py runserver
# Visit http://localhost:8000/ in your browser
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

### Code Example: Settings Configuration (myproject/settings.py)

```python
"""
Django settings for myproject project.
"""

from pathlib import Path

# Build paths inside the project
BASE_DIR = Path(__file__).resolve().parent.parent

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure-l#lav=+grjqg=vx2tx3ozn)m2voe#l#4fgw9ak)2e5^%enx5k2'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Your apps go here
    # 'myapp',
]

# Middleware processes every request/response
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'myproject.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],  # Add paths to templates directories here
        'APP_DIRS': True,  # Look for templates in app directories
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'myproject.wsgi.application'

# Database Configuration
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'

# Default primary key field type
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

### Setup Commands

```bash
# Create virtual environment
pipenv install

# Activate virtual environment
pipenv shell

# Install Django
pip install django

# Create project
django-admin startproject myproject

# Create app
python manage.py startapp myapp

# Apply migrations
python manage.py migrate

# Run development server
python manage.py runserver
```

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

### Code Example: Tour Model (asiatoursagency/models.py)

```python
from django.db import models

class Tour(models.Model):
    """Model representing a tour package"""
    # CharField for text fields with maximum length
    origin_country = models.CharField(max_length=64)
    destination_country = models.CharField(max_length=64)
    
    # IntegerField for numeric values
    number_of_nights = models.IntegerField()
    price = models.IntegerField()
    
    # String representation of the object
    def __str__(self):
        return (f"ID:{self.id}: From {self.origin_country} To {self.destination_country}, "
                f"{self.number_of_nights} nights costs ${self.price}")
    
    class Meta:
        ordering = ['price']  # Orders tours by price
        verbose_name_plural = "Tours"
```

### Admin Registration (asiatoursagency/admin.py)

```python
from django.contrib import admin
from .models import Tour

# Register the Tour model with Django admin
admin.site.register(Tour)
```

### Common Model Field Types

```python
from django.db import models

class ExampleModel(models.Model):
    # Text fields
    name = models.CharField(max_length=100)  # Short strings
    description = models.TextField()  # Long text
    
    # Numeric fields
    age = models.IntegerField()  # Whole numbers
    price = models.FloatField()  # Decimal numbers
    
    # Date/Time fields
    created_at = models.DateTimeField(auto_now_add=True)  # Auto-set on creation
    updated_at = models.DateTimeField(auto_now=True)  # Auto-update on save
    birth_date = models.DateField()
    
    # Boolean field
    is_active = models.BooleanField(default=True)
    
    # Choice field
    STATUS_CHOICES = [
        ('pending', 'Pending'),
        ('active', 'Active'),
        ('inactive', 'Inactive'),
    ]
    status = models.CharField(max_length=10, choices=STATUS_CHOICES)
    
    # Foreign Key (relationship to another model)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

### Creating and Migrating Models

```bash
# Create model in models.py, then:

# Create migration file
python manage.py makemigrations

# Apply migration to database
python manage.py migrate

# View migrations
python manage.py showmigrations

# Rollback migration
python manage.py migrate asiatoursagency 0001
```

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

### Code Example: View with Context (asiatoursagency/views.py)

```python
from django.shortcuts import render
from .models import Tour

def index(request):
    """Display all available tours"""
    # Query all tours from database
    tours = Tour.objects.all()
    
    # Prepare context data to pass to template
    context = {'tours': tours}
    
    # Render template with context
    return render(request, 'tours/index.html', context)

def tour_detail(request, tour_id):
    """Display details of a specific tour"""
    tour = Tour.objects.get(id=tour_id)
    context = {'tour': tour}
    return render(request, 'tours/detail.html', context)
```

### URL Routing (asiatoursagency/urls.py)

```python
from django.urls import path
from . import views

# Define URL patterns
urlpatterns = [
    path('', views.index, name='tour_list'),
    path('tour/<int:tour_id>/', views.tour_detail, name='tour_detail'),
]
```

### Example Template: Base Template (templates/base.html)

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Tours{% endblock %}</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        .navbar { background-color: #333; padding: 10px; }
        .navbar a { color: white; text-decoration: none; margin: 10px; }
    </style>
</head>
<body>
    <!-- Navigation bar -->
    <div class="navbar">
        <a href="{% url 'tour_list' %}">Home</a>
        <a href="{% url 'about' %}">About</a>
        <a href="{% url 'contact' %}">Contact</a>
    </div>
    
    <!-- Main content block that child templates override -->
    <div class="container">
        {% block content %}
        <p>Default content goes here</p>
        {% endblock %}
    </div>
    
    <!-- Footer -->
    <footer>
        <p>&copy; 2024 World Tour Agency. All rights reserved.</p>
    </footer>
</body>
</html>
```

### Example Template: Child Template (templates/tours/index.html)

```html
{% extends 'base.html' %}

{% block title %}Available Tours{% endblock %}

{% block content %}
    <h1>Available Tours</h1>
    
    <!-- Loop through tours -->
    {% if tours %}
        <div class="tours-list">
            {% for tour in tours %}
                <div class="tour-card">
                    <h2>{{ tour.origin_country }} to {{ tour.destination_country }}</h2>
                    
                    <!-- Display tour details -->
                    <p><strong>Nights:</strong> {{ tour.number_of_nights }} nights</p>
                    <p><strong>Price:</strong> ${{ tour.price }}</p>
                    
                    <!-- Link to tour detail page -->
                    <a href="{% url 'tour_detail' tour.id %}">View Details</a>
                </div>
            {% endfor %}
        </div>
    {% else %}
        <p>No tours available at this time.</p>
    {% endif %}
{% endblock %}
```

### Template Tags and Filters

```html
<!-- Variables -->
{{ variable_name }}

<!-- Conditional statements -->
{% if condition %}
    <p>This shows if condition is true</p>
{% elif other_condition %}
    <p>This shows if other_condition is true</p>
{% else %}
    <p>This shows if no conditions are true</p>
{% endif %}

<!-- Loops -->
{% for item in items %}
    <p>{{ item.name }}</p>
{% empty %}
    <p>No items available</p>
{% endfor %}

<!-- Filters (formatting) -->
{{ price|floatformat:2 }}  <!-- Format to 2 decimal places -->
{{ date|date:"Y-m-d" }}  <!-- Format date -->
{{ text|upper }}  <!-- Convert to uppercase -->
{{ text|truncatewords:10 }}  <!-- Truncate to 10 words -->

<!-- Template comments -->
{# This comment won't appear in HTML #}
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

### Code Example: Basic Admin Registration (asiatoursagency/admin.py)

```python
from django.contrib import admin
from .models import Tour

# Simple registration - uses default admin interface
admin.site.register(Tour)
```

### Code Example: Customized Admin (asiatoursagency/admin.py)

```python
from django.contrib import admin
from .models import Tour

class TourAdmin(admin.ModelAdmin):
    """Customized admin interface for Tour model"""
    
    # Fields to display in list view
    list_display = ['id', 'origin_country', 'destination_country', 'number_of_nights', 'price']
    
    # Fields to filter by in sidebar
    list_filter = ['price', 'number_of_nights']
    
    # Fields to search by
    search_fields = ['origin_country', 'destination_country']
    
    # Fields to display in edit form
    fields = ['origin_country', 'destination_country', 'number_of_nights', 'price']
    
    # Read-only fields
    readonly_fields = ['id']
    
    # Group fields in edit form
    fieldsets = (
        ('Tour Information', {
            'fields': ('origin_country', 'destination_country')
        }),
        ('Details', {
            'fields': ('number_of_nights', 'price')
        }),
    )
    
    # Custom action
    def make_expensive(self, request, queryset):
        """Mark selected tours as expensive (double price)"""
        queryset.update(price=models.F('price') * 2)
    make_expensive.short_description = "Double price of selected tours"
    
    actions = [make_expensive]

# Register with customization
admin.site.register(Tour, TourAdmin)
```

### Creating a Superuser

```bash
# Create superuser account
python manage.py createsuperuser

# You'll be prompted for:
# Username: admin
# Email: admin@example.com
# Password: ****
```

### Accessing Admin

1. Run development server: `python manage.py runserver`
2. Visit: `http://localhost:8000/admin/`
3. Login with superuser credentials
4. Manage your models through the interface

### Advanced Admin Features

```python
from django.contrib import admin
from django.utils.html import format_html
from .models import Tour

class TourAdmin(admin.ModelAdmin):
    # Display colored price based on value
    def colored_price(self, obj):
        if obj.price > 5000:
            color = 'red'
        elif obj.price > 2000:
            color = 'orange'
        else:
            color = 'green'
        return format_html(
            '<span style="color: {};">${}</span>',
            color,
            obj.price
        )
    colored_price.short_description = 'Price'
    
    # Method to get tour summary
    def tour_summary(self, obj):
        return f"{obj.origin_country} → {obj.destination_country} ({obj.number_of_nights}n)"
    tour_summary.short_description = 'Tour'
    
    list_display = ['tour_summary', 'colored_price', 'number_of_nights']
    
    # Show related tours count
    def get_queryset(self, request):
        queryset = super().get_queryset(request)
        return queryset.prefetch_related('bookings')

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

### Code Example: Basic Form (form_app/views.py)

```python
from django.shortcuts import render, redirect
from .form import ContactForm

# Home page view
def home_view(request):
    return render(request, 'form_app/home.html')

# Contact form view
def contact_view(request):
    """Handle contact form submission"""
    if request.method == "POST":
        # Process form submission
        form = ContactForm(request.POST)
        if form.is_valid():
            # Form data is valid, send email
            form.send_email()
            return redirect('contact-success')
    else:
        # Display empty form
        form = ContactForm()
    
    # Pass form to template
    context = {'form': form}
    return render(request, 'form_app/contact.html', context)

# Success page
def contact_success_view(request):
    return render(request, 'form_app/contact_success.html')
```

### Code Example: Custom Form Class

```python
from django import forms
from django.core.mail import send_mail

class ContactForm(forms.Form):
    """Custom form for contact messages"""
    name = forms.CharField(
        max_length=100,
        widget=forms.TextInput(attrs={
            'placeholder': 'Your Name',
            'class': 'form-control'
        })
    )
    
    email = forms.EmailField(
        widget=forms.EmailInput(attrs={
            'placeholder': 'Your Email',
            'class': 'form-control'
        })
    )
    
    subject = forms.CharField(
        max_length=200,
        widget=forms.TextInput(attrs={
            'placeholder': 'Subject',
            'class': 'form-control'
        })
    )
    
    message = forms.CharField(
        widget=forms.Textarea(attrs={
            'placeholder': 'Your Message',
            'class': 'form-control',
            'rows': 5
        })
    )
    
    # Custom validation
    def clean_email(self):
        email = self.cleaned_data.get('email')
        if not email.endswith('.com'):
            raise forms.ValidationError("Email must be a .com address")
        return email
    
    # Send email method
    def send_email(self):
        cleaned_data = self.cleaned_data
        send_mail(
            subject=cleaned_data.get('subject'),
            message=cleaned_data.get('message'),
            from_email=cleaned_data.get('email'),
            recipient_list=['admin@example.com'],
            fail_silently=False,
        )
```

### Form Template Rendering (form_app/contact.html)

```html
{% extends 'base.html' %}

{% block title %}Contact Us{% endblock %}

{% block content %}
    <h1>Contact Us</h1>
    
    <form method="POST" action="{% url 'contact' %}">
        <!-- CSRF token for security -->
        {% csrf_token %}
        
        <!-- Display form fields -->
        {% for field in form %}
            <div class="form-group">
                <label for="{{ field.id_for_label }}">{{ field.label }}</label>
                {{ field }}
                
                <!-- Display field errors -->
                {% if field.errors %}
                    <div class="error">
                        {% for error in field.errors %}
                            <p style="color: red;">{{ error }}</p>
                        {% endfor %}
                    </div>
                {% endif %}
            </div>
        {% endfor %}
        
        <!-- Non-field errors -->
        {% if form.non_field_errors %}
            <div class="error">
                {{ form.non_field_errors }}
            </div>
        {% endif %}
        
        <button type="submit" class="btn btn-primary">Send Message</button>
    </form>
{% endblock %}
```

### Model Form Example

```python
from django import forms
from .models import Product

class ProductForm(forms.ModelForm):
    """Form auto-generated from Product model"""
    
    class Meta:
        model = Product
        fields = '__all__'  # Include all fields
        
        # Custom labels for fields
        labels = {
            'product_id': 'Product ID',
            'name': 'Product Name',
            'sku': 'SKU Code',
            'price': 'Price ($)',
            'quantity': 'In Stock',
            'supplier': 'Supplier Name',
        }
        
        # Customize form widgets
        widgets = {
            'product_id': forms.NumberInput(
                attrs={'placeholder': 'e.g. 1', 'class': 'form-control'}
            ),
            'name': forms.TextInput(
                attrs={'placeholder': 'e.g. shirt', 'class': 'form-control'}
            ),
            'sku': forms.TextInput(
                attrs={'placeholder': 'e.g. S12345', 'class': 'form-control'}
            ),
            'price': forms.NumberInput(
                attrs={'placeholder': 'e.g. 19.99', 'class': 'form-control'}
            ),
            'quantity': forms.NumberInput(
                attrs={'placeholder': 'e.g. 10', 'class': 'form-control'}
            ),
            'supplier': forms.TextInput(
                attrs={'placeholder': 'e.g. ABC Corp', 'class': 'form-control'}
            ),
        }
```

### Form Field Types

```python
from django import forms

class RegistrationForm(forms.Form):
    # Text fields
    username = forms.CharField(max_length=150)
    email = forms.EmailField()
    
    # Password fields (hidden input)
    password = forms.CharField(widget=forms.PasswordInput)
    
    # Choice fields
    GENDER_CHOICES = [
        ('M', 'Male'),
        ('F', 'Female'),
        ('O', 'Other'),
    ]
    gender = forms.ChoiceField(choices=GENDER_CHOICES)
    
    # Multiple choice
    interests = forms.MultipleChoiceField(
        choices=[
            ('sports', 'Sports'),
            ('music', 'Music'),
            ('reading', 'Reading'),
        ]
    )
    
    # Boolean field (checkbox)
    agree_terms = forms.BooleanField(required=True)
    
    # Date field
    birth_date = forms.DateField(widget=forms.DateInput(attrs={'type': 'date'}))
    
    # Number field
    age = forms.IntegerField(min_value=18, max_value=100)
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

### Code Example: Registration Form (authApp/forms.py)

```python
from django import forms
from django.contrib.auth.models import User

class RegisterForm(forms.ModelForm):
    """Form for user registration with password confirmation"""
    
    # Password field with hidden input
    password = forms.CharField(widget=forms.PasswordInput)
    
    # Confirmation password field
    password_confirm = forms.CharField(
        widget=forms.PasswordInput,
        label="Confirm Password"
    )
    
    class Meta:
        model = User
        fields = ['username', 'password', 'password_confirm']
    
    def clean(self):
        """Custom validation to check if passwords match"""
        cleaned_data = super().clean()
        password = cleaned_data.get('password')
        password_confirm = cleaned_data.get('password_confirm')
        
        # Check if the passwords match
        if password and password_confirm and password != password_confirm:
            raise forms.ValidationError("Passwords do not match!")
        
        return cleaned_data


class LoginForm(forms.Form):
    """Form for user login"""
    username = forms.CharField(max_length=150)
    password = forms.CharField(widget=forms.PasswordInput)
```

### Code Example: Authentication Views (authApp/views.py)

```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required
from django.contrib.auth.models import User
from .forms import RegisterForm, LoginForm

def register_view(request):
    """Handle user registration"""
    if request.method == "POST":
        form = RegisterForm(request.POST)
        if form.is_valid():
            # Extract cleaned data
            username = form.cleaned_data.get("username")
            password = form.cleaned_data.get("password")
            
            # Create new user with hashed password
            user = User.objects.create_user(
                username=username,
                password=password
            )
            
            # Automatically log in the new user
            login(request, user)
            return redirect('home')
    else:
        form = RegisterForm()
    
    return render(request, 'accounts/register.html', {'form': form})


def login_view(request):
    """Handle user login"""
    error_message = None
    next_url = request.GET.get('next', '')
    
    if request.method == "POST":
        form = LoginForm(request.POST)
        next_url = request.POST.get('next') or 'home'
        
        if form.is_valid():
            username = form.cleaned_data.get("username")
            password = form.cleaned_data.get("password")
            
            # Authenticate user
            user = authenticate(request, username=username, password=password)
            
            if user is not None:
                # User credentials are valid
                login(request, user)
                return redirect(next_url)
            else:
                # Invalid credentials
                error_message = "Invalid username or password"
    else:
        form = LoginForm()
    
    context = {
        'form': form,
        'error': error_message,
        'next': next_url
    }
    return render(request, 'accounts/login.html', context)


def logout_view(request):
    """Handle user logout"""
    if request.method == "POST":
        logout(request)
        return redirect('login')
    else:
        return redirect('home')


# Protect view with @login_required decorator
@login_required
def home_view(request):
    """Protected home page - user must be logged in"""
    return render(request, 'auth1_app/home.html')


# Alternative: Using class-based views with LoginRequiredMixin
from django.views import View
from django.contrib.auth.mixins import LoginRequiredMixin

class ProtectedView(LoginRequiredMixin, View):
    """Protected class-based view"""
    
    # Redirect to login if user not authenticated
    login_url = 'login'
    
    def get(self, request):
        return render(request, 'registration/protected.html')
```

### Authentication in Templates

```html
<!-- Check if user is authenticated -->
{% if user.is_authenticated %}
    <p>Welcome, {{ user.username }}!</p>
    <form method="POST" action="{% url 'logout' %}">
        {% csrf_token %}
        <button type="submit">Logout</button>
    </form>
{% else %}
    <p>Please log in</p>
    <a href="{% url 'login' %}">Login</a>
    <a href="{% url 'register' %}">Register</a>
{% endif %}
```

### URL Configuration (authApp/urls.py)

```python
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.register_view, name='register'),
    path('login/', views.login_view, name='login'),
    path('logout/', views.logout_view, name='logout'),
    path('home/', views.home_view, name='home'),
]
```

### Settings Configuration for Authentication

```python
# settings.py

# Login URL (where unauthenticated users are redirected)
LOGIN_URL = 'login'

# URL to redirect after successful login
LOGIN_REDIRECT_URL = 'home'

# URL to redirect after logout
LOGOUT_REDIRECT_URL = 'login'

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        'OPTIONS': {
            'min_length': 8,
        }
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```

### User Permissions and Groups

```python
# Create a group in admin
from django.contrib.auth.models import Group, Permission

# Programmatically add user to group
user = User.objects.get(username='john')
group = Group.objects.get(name='moderators')
user.groups.add(group)

# Check if user has permission
if user.has_perm('invApp.delete_product'):
    # User can delete products
    pass

# Check if user is in group
if user.groups.filter(name='moderators').exists():
    # User is a moderator
    pass
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

### Code Example: Product Model (invApp/models.py)

```python
from django.db import models

class Product(models.Model):
    """Model representing an inventory product"""
    
    product_id = models.AutoField(primary_key=True)
    name = models.CharField(max_length=100)
    sku = models.CharField(max_length=50, unique=True)  # Unique SKU code
    price = models.FloatField()
    quantity = models.IntegerField()  # Items in stock
    supplier = models.CharField(max_length=100)
    
    # Timestamp fields (optional but recommended)
    created_at = models.DateTimeField(auto_now_add=True, null=True)
    updated_at = models.DateTimeField(auto_now=True, null=True)
    
    def __str__(self):
        """String representation of product"""
        return self.name
    
    class Meta:
        ordering = ['-updated_at']  # Most recently updated first
        verbose_name_plural = "Products"
    
    def is_low_stock(self):
        """Check if product is low in stock"""
        return self.quantity < 10
```

### Code Example: Product Form (invApp/forms.py)

```python
from django import forms
from .models import Product

class ProductForm(forms.ModelForm):
    """Form for creating and updating products"""
    
    class Meta:
        model = Product
        fields = '__all__'
        
        # Custom labels for form fields
        labels = {
            'product_id': 'Product ID',
            'name': 'Product Name',
            'sku': 'SKU Code',
            'price': 'Price ($)',
            'quantity': 'Quantity in Stock',
            'supplier': 'Supplier Name',
        }
        
        # Customize form widgets with CSS classes
        widgets = {
            'product_id': forms.NumberInput(
                attrs={
                    'placeholder': 'Auto-generated',
                    'class': 'form-control',
                    'readonly': True
                }
            ),
            'name': forms.TextInput(
                attrs={
                    'placeholder': 'e.g. Laptop, Mouse',
                    'class': 'form-control'
                }
            ),
            'sku': forms.TextInput(
                attrs={
                    'placeholder': 'e.g. SKU12345',
                    'class': 'form-control'
                }
            ),
            'price': forms.NumberInput(
                attrs={
                    'placeholder': 'e.g. 99.99',
                    'class': 'form-control',
                    'step': '0.01'
                }
            ),
            'quantity': forms.NumberInput(
                attrs={
                    'placeholder': 'e.g. 50',
                    'class': 'form-control'
                }
            ),
            'supplier': forms.TextInput(
                attrs={
                    'placeholder': 'e.g. ABC Electronics',
                    'class': 'form-control'
                }
            ),
        }
```

### Code Example: CRUD Views (invApp/views.py)

```python
from django.shortcuts import render, redirect, get_object_or_404
from django.contrib.auth.decorators import login_required
from .forms import ProductForm
from .models import Product

# Home View
def home_view(request):
    """Display home page"""
    return render(request, 'invApp/home.html')

# CREATE - Add new product
@login_required
def product_create_view(request):
    """Create a new product"""
    form = ProductForm()
    
    if request.method == 'POST':
        form = ProductForm(request.POST)
        if form.is_valid():
            # Save product to database
            form.save()
            return redirect('product_list')
    
    context = {'form': form, 'title': 'Add Product'}
    return render(request, 'invApp/product_form.html', context)

# READ - List all products
@login_required
def product_list_view(request):
    """Display list of all products"""
    # Get search query from URL parameters
    search_query = request.GET.get('search', '')
    
    # Get all products or filter by search
    if search_query:
        products = Product.objects.filter(
            name__icontains=search_query
        ) | Product.objects.filter(
            sku__icontains=search_query
        )
    else:
        products = Product.objects.all()
    
    context = {
        'products': products,
        'search_query': search_query,
        'total_products': products.count()
    }
    return render(request, 'invApp/product_list.html', context)

# READ - Get specific product details
@login_required
def product_detail_view(request, product_id):
    """Display product details"""
    product = get_object_or_404(Product, product_id=product_id)
    context = {'product': product}
    return render(request, 'invApp/product_detail.html', context)

# UPDATE - Modify existing product
@login_required
def product_update_view(request, product_id):
    """Update product information"""
    product = get_object_or_404(Product, product_id=product_id)
    form = ProductForm(instance=product)
    
    if request.method == "POST":
        form = ProductForm(request.POST, instance=product)
        if form.is_valid():
            form.save()
            return redirect('product_list')
    
    context = {'form': form, 'product': product, 'title': 'Edit Product'}
    return render(request, 'invApp/product_form.html', context)

# DELETE - Remove product from inventory
@login_required
def product_delete_view(request, product_id):
    """Delete a product"""
    product = get_object_or_404(Product, product_id=product_id)
    
    if request.method == 'POST':
        product.delete()
        return redirect('product_list')
    
    context = {'product': product}
    return render(request, 'invApp/product_confirm_delete.html', context)
```

### Code Example: URL Routing (invApp/urls.py)

```python
from django.urls import path
from . import views

urlpatterns = [
    # Home
    path('', views.home_view, name="home"),
    
    # Create
    path('create/', views.product_create_view, name="product_create"),
    
    # Read
    path('list/', views.product_list_view, name="product_list"),
    path('detail/<int:product_id>/', views.product_detail_view, name="product_detail"),
    
    # Update
    path('update/<int:product_id>/', views.product_update_view, name="product_update"),
    
    # Delete
    path('delete/<int:product_id>/', views.product_delete_view, name="product_delete"),
]
```

### Template Example: Product List (invApp/templates/invApp/product_list.html)

```html
{% extends 'invApp/base.html' %}

{% block title %}Product Inventory{% endblock %}

{% block content %}
<div class="container mt-5">
    <h1>Product Inventory</h1>
    
    <!-- Search Bar -->
    <form method="GET" class="mb-3">
        <div class="input-group">
            <input 
                type="text" 
                name="search" 
                class="form-control" 
                placeholder="Search by name or SKU..."
                value="{{ search_query }}"
            >
            <button class="btn btn-primary" type="submit">Search</button>
        </div>
    </form>
    
    <!-- Add Product Button -->
    <a href="{% url 'product_create' %}" class="btn btn-success mb-3">
        + Add New Product
    </a>
    
    <!-- Products Table -->
    {% if products %}
        <table class="table table-striped">
            <thead class="table-dark">
                <tr>
                    <th>ID</th>
                    <th>Product Name</th>
                    <th>SKU</th>
                    <th>Price</th>
                    <th>Quantity</th>
                    <th>Supplier</th>
                    <th>Status</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                {% for product in products %}
                    <tr>
                        <td>{{ product.product_id }}</td>
                        <td>{{ product.name }}</td>
                        <td>{{ product.sku }}</td>
                        <td>${{ product.price|floatformat:2 }}</td>
                        <td>
                            {% if product.is_low_stock %}
                                <span class="badge badge-warning">
                                    {{ product.quantity }} (LOW)
                                </span>
                            {% else %}
                                <span class="badge badge-success">
                                    {{ product.quantity }}
                                </span>
                            {% endif %}
                        </td>
                        <td>{{ product.supplier }}</td>
                        <td>{{ product.updated_at|date:"Y-m-d H:i" }}</td>
                        <td>
                            <!-- Edit Button -->
                            <a href="{% url 'product_update' product.product_id %}" 
                               class="btn btn-sm btn-info">
                                Edit
                            </a>
                            
                            <!-- Delete Button -->
                            <a href="{% url 'product_delete' product.product_id %}" 
                               class="btn btn-sm btn-danger">
                                Delete
                            </a>
                        </td>
                    </tr>
                {% endfor %}
            </tbody>
        </table>
        
        <!-- Summary -->
        <p><strong>Total Products:</strong> {{ total_products }}</p>
    {% else %}
        <div class="alert alert-info">
            No products found. <a href="{% url 'product_create' %}">Add one now</a>
        </div>
    {% endif %}
</div>
{% endblock %}
```

### Running the Project

```bash
# Navigate to project directory
cd FinalProject/invProject

# Install dependencies
pipenv install

# Activate virtual environment
pipenv shell

# Run migrations
python manage.py migrate

# Create superuser for admin access
python manage.py createsuperuser

# Start development server
python manage.py runserver

# Visit the application
# Home: http://localhost:8000/
# Admin: http://localhost:8000/admin/
```

### Key Features Implemented

1. **CRUD Operations:** Complete Create, Read, Update, Delete functionality
2. **Authentication:** User login required to access inventory
3. **Search Functionality:** Search products by name or SKU
4. **Data Validation:** Forms validate product data before saving
5. **Template Inheritance:** Consistent UI across all pages
6. **Admin Interface:** Full Django admin support
7. **Error Handling:** Proper error messages and user feedback
8. **Responsive Design:** Mobile-friendly interface

### Database Schema

```
Product Table
├── product_id (Primary Key, Auto-increment)
├── name (String, Max 100 chars)
├── sku (String, Unique, Max 50 chars)
├── price (Float)
├── quantity (Integer)
├── supplier (String, Max 100 chars)
├── created_at (DateTime, Auto-set)
└── updated_at (DateTime, Auto-update)
```

### Technology Stack
- **Framework:** Django 3.x/4.x
- **Database:** SQLite3
- **Frontend:** HTML5, CSS3, Bootstrap (optional)
- **Python:** 3.8+

### Security Features
- CSRF token protection on all forms
- Password hashing for user authentication
- Login required decorators on protected views
- SQL injection prevention through ORM
- XSS protection in templates

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
