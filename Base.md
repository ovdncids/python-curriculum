# Base.html
base.html
```py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Title</title>
    {% load static %}
    <link href="{% static 'base.css' %}" rel="stylesheet">
    {% block css %}
    {% endblock css %}
</head>
<body>
    <div class="wrap">
        {% block content %}
        {% endblock content %}
    </div>
</body>
</html>
```

home.py
```py
{% extends 'base.html' %}

{% block css %}{% load static %}
<!-- <link href="{% static 'home.css' %}" rel="stylesheet"> -->
{% endblock css %}

{% block content %}
Home
{% endblock content %}
```
