# Django REST
https://cjh5414.github.io/django-rest-framework/

## Django REST 설치
```sh
# pip install django
pip install djangorestframework
```

## Init
```sh
django-admin startproject djangoRestTutorial
```

.gitignore
```gitignore
.DS_Store

# Editor directories and files
.idea
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw*

# __pycache__
__pycache__

# db.sqlite3
db.sqlite3

```

## Startapp: CRUD
```sh
python3 manage.py startapp crud
```

## Settings
/djangoRestTutorial/settings.py
```py
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'crud',
]

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        # 'rest_framework.permissions.IsAdminUser',
    ]
}

```

## Models
/crud/models.py
```py
class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```

## Serializers
/crud/serializers.py
```py
from crud.models import Person
from rest_framework import serializers

class PersonSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Person
        fields = ('first_name', 'last_name')

```

## Viewer
/crud/viewes.py
```py
from rest_framework import viewsets
from crud.serializers import PersonSerializer
from crud.models import Person

class PersonViewSet(viewsets.ModelViewSet):
    queryset = Person.objects.all()
    serializer_class = PersonSerializer

```

## URLs
/djangoRestTutorial/urls.py
```py
from django.conf.urls import url, include
from rest_framework import routers
from crud import views

router = routers.DefaultRouter()
router.register(r'persons', views.PersonViewSet)

urlpatterns = [
    # ...
    url(r'^', include(router.urls)),
    url(r'^api-auth/', include('rest_framework.urls', namespace='rest_framework')),
]
```

## Migrations
```sh
python3 manage.py makemigrations
python3 manage.py migrate
```

## Set: Default JSON
/djangoRestTutorial/settings.py
```py
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': (
        'rest_framework.renderers.JSONRenderer',
    ),
    'DEFAULT_PARSER_CLASSES': (
        'rest_framework.parsers.JSONParser',
    )
}
```

## Run
```sh
python3 manage.py runserver
```
