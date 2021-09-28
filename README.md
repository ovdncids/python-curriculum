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

python {Location: 경로/site-packages}../Scripts/django-admin --version
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

# debug 모드가 실행 된다면 VSCode를 다시 실행 시켜서, debug 모드가 실행 되는지 확인
```

## Members 앱 생성
```sh
python manage.py startapp members
```

### Members 앱 페이지 만들기
members/views.py
```py
from django.shortcuts import render, redirect
from django.http import HttpResponse

def members_read(request):
    return HttpResponse("Hello, world.")

def root(request):
    return redirect('members/')
```

### Members 앱 페이지와 라우터 연결
django_study/urls.py
```py
from members import views as views

urlpatterns = [
    path('members/', views.members_read, name='members'),
    path('', views.root),
```

### Members 앱 페이지와 HTML 연결
members/views.py
```diff
- return HttpResponse("Hello, world.")
```
```py
return render(request, 'members.html')
```

members/templates/members.html
```html
Hello, world.
```

django_study/settings.py
```py
INSTALLED_APPS = [
    'members',
```

### Members 앱 Markup
members/templates/members.html
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
                    <li><h2>Members</h2></li>
                    <li><h2>Search</h2></li>
                </ul>
            </nav>
            <hr />
            <section class="contents">
                <div>
                    <h3>Members</h3>
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

members/static/index.css
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

### Members 앱 Header, Nav, Footer 나누기
members/templates/members.html
```diff
- <header>
-     <h1>Django study</h1>
- </header>

- <nav class="nav">
-     <ul>
-         <li><h2>Members</h2></li>
-         <li><h2>Search</h2></li>
-     </ul>
- </nav>

- <footer>Copyright</footer>
```
```py
{% include "include/header.html" %}
```

members/templates/include/header.html
```html
<header>
    <h1>Django study</h1>
</header>
```

### Members 앱 Search 페이지 만들기
members/views.py
```py
def search(request):
    return render(request, 'search.html')
```

members/templates/search.html
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

members/views.py
```diff
- return render(request, 'members.html')
- return render(request, 'search.html')
```
```py
return render(request, 'members.html', {'active_members': 'active'})
return render(request, 'search.html', {'active_search': 'active'})
```

members/templates/include/nav.html
```py
<li><h2><a href="{% url 'members' %}" class="{{active_members}}">Members</a></h2></li>
<li><h2><a href="{% url 'search' %}" class="{{active_search}}">Search</a></h2></li>
```

### Members 앱 Create
members/views.py
```py
members = []

def members_create(request):
    members.append({
      'name': request.POST['name'],
      'age': request.POST['age'],
    })
    print('Done members_create', members)
    return redirect('members/')
```

django_study/urls.py
```py
urlpatterns = [
    path('members_create', views.members_create, name='members_create'),
```

members/templates/members.html
```diff
- <div>
-     <h3>Members</h3>
-     <p>Contents</p>
- </div>
```
```py
<div>
    <h3>Members</h3>
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
    <form method="post" action="{% url 'members_create' %}">
        {% csrf_token %}
        <h4>Create</h4>
        <input type="text" name="name" placeholder="Name" />
        <input type="text" name="age" placeholder="Age" />
        <button>Create</button>
    </form>
</div>
```

### Members 앱 Read
members/views.py
```diff
- members = []
```
```py
members = [{
    'name': '홍길동',
    'age': 20
}, {
    'name': '춘향이',
    'age': 16
}]
```
```diff
- return render(request, 'members.html', {'active_members': 'active'})
```
```py
return render(request, 'members.html', {
    'active_members': 'active',
    'members': members,
})
```

members/templates/members.html
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
{% for member in members %}
<tr>
    <td>{{member.name}}</td>
    <td>{{member.age}}</td>
    <td>
        <button>Update</button>
        <button>Delete</button>
    </td>
</tr>
{% endfor %}
```

### Members 앱 Update
members/views.py
```py
def members_update(request, index):
    members[index] = {
      'name': request.POST['name'],
      'age': request.POST['age'],
    }
    print('Done members_update', members)
    return redirect('/members/')
```

django_study/urls.py
```py
urlpatterns = [
    path('members_update/<int:index>', views.members_update, name='members_update'),
```

members/templates/members.html
```diff
- {% for member in members %}
- <tr>
-     <td>{{member.name}}</td>
-     <td>{{member.age}}</td>
-     <td>
-         <button>Update</button>
-         <button>Delete</button>
-     </td>
- </tr>
- {% endfor %}
```
```py
{% for member in members %}
<form method="post">
    {% csrf_token %}
    <tr>
        <td><input type="text" name="name" value="{{member.name}}" placeholder="Name" /></td>
        <td><input type="text" name="age" value="{{member.age}}" placeholder="Age" /></td>
        <td>
            <button onclick=this.form.action='{% url "members_update" forloop.counter0 %}'>Update</button>
            <button>Delete</button>
        </td>
    </tr>
</form>
{% endfor %}
```

### Members 앱 Delete
members/views.py
```py
def members_delete(request, index):
    del members[index]
    print('Done members_delete', members)
    return redirect('/members/')
```

django_study/urls.py
```py
urlpatterns = [
    path('members_delete/<int:index>', views.members_delete, name='members_delete'),
```

members/templates/members.html
```diff
- <button>Delete</button>
```
```py
<button onclick=this.form.action='{% url "members_delete" forloop.counter0 %}'>Delete</button>
```

## Members Database 생성
members/models.py
```py
class Member(models.Model):
    name = models.CharField(max_length=200)
    age = models.IntegerField(default=0)

    def __str__(self):
        return self.name + ', ' + str(self.age)
```

### Members Database Migration
```sh
python manage.py makemigrations members
```
* members/migrations/0001_initial.py 파일이 생성됨

```sh
python manage.py migrate
# Migration 적용 확인
python manage.py showmigrations members
```
* `members/migrations/0001_initial.py`을 바탕으로 Database정보를 `db.sqlite3` 파일에 입력함
* ❕ 만약 Migration 도중 에러가 난다면 `db.sqlite3` 또는 `members/migrations/0001_initial.py` 파일을 지우고 다시 실행 해야함

### Members Database Terminal에서 CRUD
```sh
# /django_tutorial/settings.py 파일을 import 하고 python을 실행한 것과 같다.
python manage.py shell
```
```py
from members.models import Member

# Create
member = Member(name='홍길동', age='20')
member
member.save()
member = Member(name='춘향이', age='16')
member.save()

# 현재 DB의 정보 받아 오기
Member.objects.all()

# Read
member = Member.objects.get(id=1)
member.name
member.age

# Update
member.name = '이순신'
member.age = 32
member.save()

# Delete
member.delete()

# Search Members
Member.objects.filter(name='춘향이')
Member.objects.filter(name__contains='향').count()
```

* ❕ `.save()` 또는 `.delete()` 메소드를 실행해야 DB에 적용됨
* VSCode에서 SQLite 설치
```
Ctrl(Command) + p
>SQLite: Open Database
# db.sqlite3 선택
# 왼쪽 SQLITE EXPLORER > db.sqlite3 > members_members > Show Table

>SQLite: Close Database
```

### Members Database Read
members/views.py
```diff
- members = [{
-     'name': '홍길동',
-     'age': 20
- }, {
-     'name': '춘향이',
-     'age': 16
- }]
```
```py
from .models import Member
```
```diff
def members_read(request):
-   'members': members,
+   'members': Member.objects.all(),
```

### Members Database Create
members/views.py
```diff
- def members_create(request):
```
```py
def members_create(request):
    id = Member.objects.create(
      name = request.POST['name'],
      age = request.POST['age'],
    )
    print('Done members_create', Member.objects.get(id=id.pk))
    return redirect('members/')
```

### Members Database Update
members/views.py
```diff
- def members_update(request, index):
```
```py
def members_update(request, index):
    member = Member.objects.get(id=index)
    member.name = request.POST['name']
    member.age = request.POST['age']
    member.save()
    print('Done members_update', member)
    return redirect('/members/')
```

members/templates/members.html
```diff
- forloop.counter0
+ member.id
```

### Members Database Delete
members/views.py
```diff
- def members_delete(request, index):
```
```py
def members_delete(request, index):
    member = Member.objects.get(id=index)
    member.delete()
    print('Done members_delete', member)
    return redirect('/members/')
```

### Search Database
members/views.py
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
      'members': Member.objects.filter(name__contains=q),
    })
```

members/templates/search.html
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
                {% for member in members %}
                <tr>
                    <td>{{member.name}}</td>
                    <td>{{member.age}}</td>
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

members/admin.py
```py
from .models import Member

admin.site.register(Member)
```

http://127.0.0.1:8000/admin
