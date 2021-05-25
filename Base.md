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
    {% block static %}
    {% endblock static %}
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

{% block static %}{% load static %}
<!-- <link href="{% static 'home.css' %}" rel="stylesheet"> -->
{% endblock static %}

{% block content %}
Home
{% endblock content %}
```
