# Django

## 자주쓰는 명령어
```py
python manage.py runserver
python manage.py makemigrations
python manage.py migrate
```

## Django 설치
https://www.djangoproject.com/download/
```sh
pip install django==3.2
# OR
pipenv install django
```

## Django 확인
https://docs.djangoproject.com/ko/2.1/intro/install/
```sh
python -m django --version
# OR
django-admin --version
```

### django-admin 실행이 안 된다면
```sh
pip list
  # 설치된 패키지 리스트를 볼 수 있다.
pip show django
  # Django의 설치 정보, 경로등을 볼 수 있다. (Location 정보가 중요)

{Location: 경로/site-packages}../Scripts/django-admin --version
```

## 프로젝트 생성
https://docs.djangoproject.com/ko/2.1/intro/tutorial01/
```sh
django-admin startproject django_study
cd django_study
code .
```

## GIT
```sh
git init
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

# pyenv
.python-version

# pipenv
Pipfile
Pipfile.lock
```

## 서버 실행
```sh
python manage.py runserver
```

## VSCode debug 모드
https://code.visualstudio.com/docs/python/tutorial-django

```sh
# VSCode 확장: Python 설치 되었는지 확인
# pipenv가 설치 되었을 경우 현재 버전 확인
  pipenv --venv
    # 새로운 터미널에서 버전 확인만 하고 끄자: pipenv shell 실행 전의 명령은 무조건 pyenv의 영향을 받는다.

VSCode -> Ctrl(Command) + Shift + p -> >Python: Select Interpreter -> 올바른 버전 선택
  # VSCode 왼쪽 하단의 선택된 python 정보가 올바른지 확인
디버그 탭 -> launch.json 만들기 -> Python -> Django
  .vscode/launch.json 파일이 생성됨
  디버깅 시작 버튼 누르기
  # 안되면: Django 서버 실행 되는지, python 버전 맞는지 확인
  # ${workspaceFolder}\manage.py <- 경로가 맞는지 

# debug 모드가 실행 된다면 VSCode를 다시 실행 시켜서, debug 모드가 실행 되는지 확인
```

## Users 앱 생성
```sh
python manage.py startapp users
```

### Users 앱 페이지 만들기
users/views.py
```py
from django.shortcuts import render, redirect
from django.http import HttpResponse

def users_read(request):
    return HttpResponse("Hello, world.")

def root(request):
    return redirect('users/')
```

### Users 앱 페이지와 라우터 연결
django_study/urls.py
```py
from users import views as views

urlpatterns = [
    path('users/', views.users_read, name='users'),
    path('', views.root),
```

### Users 앱 페이지와 HTML 연결
users/views.py
```diff
- return HttpResponse("Hello, world.")
```
```py
return render(request, 'users.html')
```

users/templates/users.html
```html
Hello, world.
```

django_study/settings.py
```py
INSTALLED_APPS = [
    'users',
```

### Users 앱 Markup
users/templates/users.html
```py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Django study</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <div>
        <header>
            <h1>Django study</h1>
        </header>
        <hr />
        <div class="container">
            <nav class="nav">
                <ul>
                    <li><h2>Users</h2></li>
                    <li><h2>Search</h2></li>
                </ul>
            </nav>
            <hr />
            <section class="contents">
                <div>
                    <h3>Users</h3>
                    <p>Contents</p>
                </div>
            </section>
            <hr />
        </div>
        <footer>Copyright</footer>
    </div>
</body>
</html>
```

users/static/index.css
```css
* {
    margin: 0;
    font-family: -apple-system,BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
a:link, a:visited {
    text-decoration: none;
    color: black;
}
a.active {
    color: white;
}
hr {
    display: none;
}
h1, footer, .nav ul {
    padding: 0.5rem;
}
h4, li {
    margin: 0.5rem 0;
}
hr {
    margin: 1rem 0;
}
hr {
    border: 0;
    border-top: 1px solid #ccc;
}
input[type=text] {
    width: 120px;
}

.d-block {
    display: block;
}
.container {
    display: flex;
    border-top: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
}
.nav {
    min-height: 300px;
    background-color: #4285F4;
}
.nav ul {
    list-style: none;
}
.contents {
    flex: 1;
    padding: 1rem;
}

.table-search {
    border: 1px solid rgb(118, 118, 118);
    border-collapse: collapse;
    text-align: center;
}
.table-search th, .table-search td {
    padding: 0.2rem;
}
.table-search td {
    border-top: 1px solid rgb(118, 118, 118);
    min-width: 100px;
}
```

```sh
"GET /static/index.css HTTP/1.1" 404
# 404가 나오면 서버 재시작
```

### Users 앱 Header, Nav, Footer 나누기
users/templates/users.html
```diff
- <header>
-     <h1>Django study</h1>
- </header>

- <nav class="nav">
-     <ul>
-         <li><h2>Users</h2></li>
-         <li><h2>Search</h2></li>
-     </ul>
- </nav>

- <footer>Copyright</footer>
```
```py
{% include "include/header.html" %}
```

users/templates/include/header.html
```html
<header>
    <h1>Django study</h1>
</header>
```

### Users 앱 Search 페이지 만들기
users/views.py
```py
def search(request):
    return render(request, 'search.html')
```

users/templates/search.html
```py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Django study</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <div>
        {% include "include/header.html" %}
        <hr />
        <div class="container">
            {% include "include/nav.html" %}
            <hr />
            <section class="contents">
                <div>
                    <h3>Search</h3>
                    <p>Contents</p>
                </div>
            </section>
            <hr />
        </div>
        {% include "include/footer.html" %}
    </div>
</body>
</html>
```

django_study/urls.py
```py
urlpatterns = [
    path('search/', views.search, name='search'),
```

**주소 창에서 URL 경로 바꾸어 보기**

users/views.py
```diff
- return render(request, 'users.html')
- return render(request, 'search.html')
```
```py
return render(request, 'users.html', {'active_users': 'active'})
return render(request, 'search.html', {'active_search': 'active'})
```

users/templates/include/nav.html
```py
<li><h2><a href="{% url 'users' %}" class="{{active_users}}">Users</a></h2></li>
<li><h2><a href="{% url 'search' %}" class="{{active_search}}">Search</a></h2></li>
```

### Users 앱 Create
users/views.py
```py
users = []

def users_create(request):
    users.append({
      'name': request.POST['name'],
      'age': request.POST['age'],
    })
    print('Done users_create', users)
    return redirect('users/')
```

django_study/urls.py
```py
urlpatterns = [
    path('users_create', views.users_create, name='users_create'),
```

users/templates/users.html
```diff
- <div>
-     <h3>Users</h3>
-     <p>Contents</p>
- </div>
```
```py
<div>
    <h3>Users</h3>
    <hr class="d-block" />
    <div>
        <h4>Read</h4>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Age</th>
                    <th>Modify</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>홍길동</td>
                    <td>20</td>
                    <td>
                        <button>Update</button>
                        <button>Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <hr class="d-block" />
    <form method="post" action="{% url 'users_create' %}">
        {% csrf_token %}
        <h4>Create</h4>
        <input type="text" name="name" placeholder="Name" />
        <input type="text" name="age" placeholder="Age" />
        <button>Create</button>
    </form>
</div>
```

### Users 앱 Read
users/views.py
```diff
- users = []
```
```py
users = [{
    'name': '홍길동',
    'age': 20
}, {
    'name': '춘향이',
    'age': 16
}]
```
```diff
- return render(request, 'users.html', {'active_users': 'active'})
```
```py
return render(request, 'users.html', {
    'active_users': 'active',
    'users': users,
})
```

users/templates/users.html
```diff
- <tr>
-     <td>홍길동</td>
-     <td>20</td>
-     <td>
-         <button>Update</button>
-         <button>Delete</button>
-     </td>
- </tr>
```
```py
{% for user in users %}
<tr>
    <td>{{user.name}}</td>
    <td>{{user.age}}</td>
    <td>
        <button>Update</button>
        <button>Delete</button>
    </td>
</tr>
{% endfor %}
```

### Users 앱 Update
users/views.py
```py
def users_update(request, index):
    users[index] = {
      'name': request.POST['name'],
      'age': request.POST['age'],
    }
    print('Done users_update', users)
    return redirect('/users/')
```

django_study/urls.py
```py
urlpatterns = [
    path('users_update/<int:index>', views.users_update, name='users_update'),
```

users/templates/users.html
```diff
- {% for user in users %}
- <tr>
-     <td>{{user.name}}</td>
-     <td>{{user.age}}</td>
-     <td>
-         <button>Update</button>
-         <button>Delete</button>
-     </td>
- </tr>
- {% endfor %}
```
```py
{% for user in users %}
<form method="post">
    {% csrf_token %}
    <tr>
        <td><input type="text" name="name" value="{{user.name}}" placeholder="Name" /></td>
        <td><input type="text" name="age" value="{{user.age}}" placeholder="Age" /></td>
        <td>
            <button onclick=this.form.action='{% url "users_update" forloop.counter0 %}'>Update</button>
            <button>Delete</button>
        </td>
    </tr>
</form>
{% endfor %}
```

### Users 앱 Delete
users/views.py
```py
def users_delete(request, index):
    del users[index]
    print('Done users_delete', users)
    return redirect('/users/')
```

django_study/urls.py
```py
urlpatterns = [
    path('users_delete/<int:index>', views.users_delete, name='users_delete'),
```

users/templates/users.html
```diff
- <button>Delete</button>
```
```py
<button onclick=this.form.action='{% url "users_delete" forloop.counter0 %}'>Delete</button>
```

## Users Database 생성
users/models.py
```py
class User(models.Model):
    name = models.CharField(max_length=200)
    age = models.IntegerField(default=0)

    def __str__(self):
        return self.name + ', ' + str(self.age)
```

### Users Database Migration
```sh
python manage.py makemigrations users
```
* users/migrations/0001_initial.py 파일이 생성됨

```sh
python manage.py migrate
# Migration 적용 확인
python manage.py showmigrations users
```
* `users/migrations/0001_initial.py`을 바탕으로 Database정보를 `db.sqlite3` 파일에 입력함
* ❕ 만약 Migration 도중 에러가 난다면 `db.sqlite3` 또는 `users/migrations/0001_initial.py` 파일을 지우고 다시 실행 해야함

### Users Database Terminal에서 CRUD
```sh
# /django_tutorial/settings.py 파일을 import 하고 python을 실행한 것과 같다.
python manage.py shell
```
```py
from users.models import User

# Create
user = User(name='홍길동', age='20')
user
user.save()
user = User(name='춘향이', age='16')
user.save()

# 현재 DB의 정보 받아 오기
User.objects.all()

# Read
user = User.objects.get(id=1)
user.name
user.age

# Update
user.name = '이순신'
user.age = 32
user.save()

# Delete
user.delete()

# Search Users
User.objects.filter(name='춘향이')
User.objects.filter(name__contains='향').count()
```

* ❕ `.save()` 또는 `.delete()` 메소드를 실행해야 DB에 적용됨
* VSCode에서 SQLite 설치
```
Ctrl(Command) + p
>SQLite: Open Database
# db.sqlite3 선택
# 왼쪽 SQLITE EXPLORER > db.sqlite3 > users_users > Show Table

>SQLite: Close Database
```

### Users Database Read
users/views.py
```diff
- users = [{
-     'name': '홍길동',
-     'age': 20
- }, {
-     'name': '춘향이',
-     'age': 16
- }]
```
```py
from .models import User
```
```diff
def users_read(request):
-   'users': users,
+   'users': User.objects.all(),
```

### Users Database Create
users/views.py
```diff
- def users_create(request):
```
```py
def users_create(request):
    id = User.objects.create(
      name = request.POST['name'],
      age = request.POST['age'],
    )
    print('Done users_create', User.objects.get(id=id.pk))
    return redirect('users/')
```

### Users Database Update
users/views.py
```diff
- def users_update(request, index):
```
```py
def users_update(request, index):
    user = User.objects.get(id=index)
    user.name = request.POST['name']
    user.age = request.POST['age']
    user.save()
    print('Done users_update', user)
    return redirect('/users/')
```

users/templates/users.html
```diff
- forloop.counter0
+ user.id
```

### Users Database Delete
users/views.py
```diff
- def users_delete(request, index):
```
```py
def users_delete(request, index):
    user = User.objects.get(id=index)
    user.delete()
    print('Done users_delete', user)
    return redirect('/users/')
```

### Search Database
users/views.py
```diff
- def search(request):
```
```py
def search(request):
    q = request.GET.get('q', '')
    print(q)
    return render(request, 'search.html', {
      'active_search': 'active',
      'q': q,
      'users': User.objects.filter(name__contains=q),
    })
```

users/templates/search.html
```diff
- <div>
-     <h3>Search</h3>
-     <p>Contents</p>
- </div>
```
```py
<div>
    <h3>Search</h3>
    <hr class="d-block" />
    <div>
        <form>
            <input type="text" placeholder="Search" name="q" value="{{q}}" />
            <button>Search</button>
        </form>
    </div>
    <hr class="d-block" />
    <div>
        <table class="table-search">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Age</th>
                </tr>
            </thead>
            <tbody>
                {% for user in users %}
                <tr>
                    <td>{{user.name}}</td>
                    <td>{{user.age}}</td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
    </div>
</div>
```

## Admin 페이지 만들기
```sh
python manage.py createsuperuser
```

users/admin.py
```py
from .models import User

admin.site.register(User)
```

http://127.0.0.1:8000/admin
