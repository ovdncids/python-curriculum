<!-- # Python

## Windows 설치
https://docs.djangoproject.com/ko/2.1/howto/windows/

## Homebrew 설치
https://brew.sh/index_ko
```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Python3 설치
```sh
brew install python3
```

## pip (Python Index Package) 설치
https://pip.pypa.io/en/stable/installing/#upgrading-pip
```sh
# pip 버전 올리기 (현재 버전 18.1)
python3 -m pip install -U pip
```

## pylint 설치
```sh
python3 -m pip install -U pylint --user
``` -->

# Django

## Django 추천 버전
https://docs.djangoproject.com/ko/2.1/faq/install/#faq-python-version-support

## Django 설치
https://www.djangoproject.com/download/
```sh
pip install Django==3.2
# OR
pipenv install django
```

## Django 확인
https://docs.djangoproject.com/ko/2.1/intro/install/
```sh
python
>>>
import django
print(django.get_version())
```

```sh
python -m django --version
# OR
django-admin --version
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
```

## 서버 실행
```sh
python manage.py runserver
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
-   <h1>Django study</h1>
- </header>

- <nav class="nav">
-   <ul>
-     <li><h2>Members</h2></li>
-     <li><h2>Search</h2></li>
-   </ul>
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
-   <h3>Members</h3>
-   <p>Contents</p>
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
-   <td>홍길동</td>
-   <td>20</td>
-   <td>
-     <button>Update</button>
-     <button>Delete</button>
-   </td>
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
-   <td>{{member.name}}</td>
-   <td>{{member.age}}</td>
-   <td>
-     <button>Update</button>
-     <button>Delete</button>
-   </td>
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
class Members(models.Model):
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
```
* `members/migrations/0001_initial.py`을 바탕으로 Database정보를 `db.sqlite3` 파일에 입력함
* ❕ 만약 Migration 도중 에러가 난다면 `db.sqlite3` 또는 `members/migrations/0001_initial.py` 파일을 지우고 다시 실행 해야함

### Members Database Terminal에서 CRUD
```sh
# /django_tutorial/settings.py 파일을 import 하고 python을 실행한 것과 같다.
python manage.py shell
```
```py
from members.models import Members

# All Members
Members.objects.all()

# Create
member = Members(name='홍길동', age='20')
member.save()
member = Members(name='춘향이', age='16')
member.save()

# Read
member = Members.objects.get(id=1)
member.name
member.age

# Update
member.name = '이순신'
member.age = 32
member.save()

# Delete
member.delete()
```

* VSCode에서 SQLite 설치
```
Ctrl(Command) + p
>SQLite: Open Database
# db.sqlite3 선택
# 왼쪽 SQLITE EXPLORER > db.sqlite3 > members_members > Show Table

>SQLite: Close Database
```










## Database Setting
https://docs.djangoproject.com/ko/2.1/ref/settings/#std:setting-DATABASES

### MySQL DB API Drivers
https://docs.djangoproject.com/ko/2.1/ref/databases/#mysql-db-api-drivers

```sh
pip install mysqlclient
```

#### 윈도우에서 설치가 안될 경우
http://lemontia.tistory.com/756

https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysqlclient

python이 32비트인지 64인지 확인 후에 mysqlclient-1.3.13-cp37-cp37m-win32.whl 다운로드

```cmd
# 다운 받은 경로에서
pip install mysqlclient-1.3.13-cp37-cp37m-win32.whl
```

/django_study/settings.py
```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```


## Migrate 실행
https://docs.djangoproject.com/ko/2.1/intro/tutorial02/
```sh
python manage.py migrate

# mysql>
SHOW DATABASES;
USE django_study;
SHOW TABLES;
# mysql>
```

## Members 모델 생성
/members/models.py
```py
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
        # models.CASCADE는 부모인 Question 레코드가 지워지면 자식인 Choice 레코드 모두를 지우겠다는 뜻이다.
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

```

## Members 모델 활성화
/django_study/settings.py
```py
INSTALLED_APPS = [
    'members.apps.MembersConfig',
```

migrations 등록
```sh
python manage.py makemigrations members
```

실행될 SQL문 확인
```sh
python manage.py sqlmigrate members 0001
```

Migrate 실행
```sh
python manage.py migrate
```

## Terminal에서 django 명령 실행 시키기
```sh
# /django_study/settings.py 파일을 import 하고 python을 실행한 것과 같다.
python manage.py shell
```

```py
from members.models import Choice, Question

# question 개수 0개
Question.objects.all()

from django.utils import timezone

q = Question(question_text="What's new?", pub_date=timezone.now())
q
q.save() # DB 해당 레코드 생성

# mysql>
SELECT * FROM members_question;
# mysql>

q.id
q.question_text
q.pub_date
q.question_text = "What's up?"
q.save()

# mysql>
SELECT * FROM members_question;
# mysql>

# question 개수 1개
Question.objects.all()
```

### Members 모델에서 사용가능한 함수 추가
/members/models.py
```py
import datetime
from django.utils import timezone

class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

class Choice(models.Model):
    # ...
    def __str__(self):
        return self.choice_text

```

```sh
python manage.py shell
```

```py
from members.models import Choice, Question

Question.objects.all()
Question.objects.filter(id=1)
Question.objects.filter(question_text__startswith='What')

from django.utils import timezone
current_year = timezone.now().year
Question.objects.get(pub_date__year=current_year)

Question.objects.get(id=2) # 에러 발생

Question.objects.get(pk=1)
q = Question.objects.get(pk=1)
q.was_published_recently()

q.choice_set.all()
q.choice_set.create(choice_text='Not much', votes=0)

# mysql>
SELECT * FROM members_choice;
# mysql>

q.choice_set.create(choice_text='The sky', votes=0)
c = q.choice_set.create(choice_text='Just hacking again', votes=0)
c.question

q.choice_set.all()
q.choice_set.count()
Choice.objects.filter(question__pub_date__year=current_year)

c = q.choice_set.filter(choice_text__startswith='Just hacking')
c.delete() # DB 해당 레코드 삭제
```

## Members Admin에 등록

### Admin user 등록
```sh
python manage.py createsuperuser
```
```sql
# mysql>
SELECT * FROM auth_user;
```

/members/admin.py
```py
from .models import Question

admin.site.register(Question)
```

http://127.0.0.1:8000/admin

## Members views.py 라우터 등록
/members/views.py
```py
def detail(request, question_id):
    return HttpResponse("You're lokking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)

```

/members/urls.py
```py
urlpatterns = [
    # ex: /members/
    path('', views.index, name='index'),
    # ex: /members/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # ex: /members/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # ex: /members/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),
]

```

## Members template view 적용
/members/views.py
```py
from django.template import loader
from .models import Question

def index(request):
    lastes_question_list = Question.objects.order_by('-pub_date')[:5]
        # '-pub_date' = 내림차순(DESC), 'pub_date' = 오름차순(ASC)
        # [:5] = 정렬순서에서 5개까지 레코드를 읽는다.
        # [0] = 첫번째 레코드만 읽는다.
    template = loader.get_template('members/index.html')
    context = {
        'latest_question_list': lastes_question_list,
    }
    return HttpResponse(template.render(context, request))

```

/members/templates/members/index.html
```py
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/members/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No members are available.</p>
{% endif %}

```

## Members shortcuts render 적용
/members/views.py
```diff
- from django.template import loader
- template = loader.get_template('members/index.html')
- return HttpResponse(template.render(context, request))
+ return render(request, 'members/index.html', context)
```

## Members http404
/members/views.py
```py
from django.http import Http404

def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404('Question does not exist')
    return render(request, 'members/detail.html', {'question': question})
```

/members/template/members/detail.html
```py
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>

```

## Members shortcuts 404
/members/views.py
```diff
- from django.shortcuts import render
+ from django.shortcuts import get_object_or_404, render
- from django.http import Http404

- try:
-     question = Question.objects.get(pk=question_id)
- except Question.DoesNotExist:
-     raise Http404('Question does not exist')
+ question = get_object_or_404(Question, pk=question_id)
```

## Members remove URL: /members
/members/template/index.html
```diff
- <li><a href="/members/{{ question.id }}/">{{ question.question_text }}</a></li>
+ <li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```

/members/urls.py
```diff
- path('<int:question_id>/', views.detail, name='detail'),
+ path('detail/<int:question_id>/', views.detail, name='detail'),
    # 확인 후에 path('<int:question_id>/', views.detail, name='detail'), 되돌린다.
```

## Members route namespace 적용
/members/urls.py
```py
app_name = 'members'
# urlpatterns = [ ...
```

/members/template/index.html
```diff
- <li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
+ <li><a href="{% url 'members:detail' question.id %}">{{ question.question_text }}</a></li>
```

## Members detail form 만들기
/members/template/detail.html
```py
<h1>{{ question.question_text }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'members:vote' question.id %}" method="post">
{% csrf_token %}
{% for choice in question.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br>
{% endfor %}
<input type="submit" value="Vote">
</form>

```

## Members vote, results 만들기
/members/views.py
```diff
- from django.http import HttpResponse
+ from django.http import HttpResponseRedirect
+ from django.urls import reverse
- from .models import Question
+ from .models import Choice, Question
```
```py
def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'members/results.html', {'question': question})

def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'members/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('members:results', args=(question.id,)))

```

/members/template/members/results.html
```py
<h1>{{ question.question_text }}</h1>

<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
{% endfor %}
</ul>

<a href="{% url 'members:detail' question.id %}">Vote again?</a>

```

## Members generic view
/members/views.py 안에 함수를 클래스화 한다.

/members/urls.py
```diff
- path('', views.index, name='index'),
+ path('', views.IndexView.as_view(), name='index'),

- path('<int:question_id>/', views.detail, name='detail'),
+ path('<int:pk>/', views.DetailView.as_view(), name='detail'),

- path('<int:question_id>/results/', views.results, name='results'),
+ path('<int:pk>/results/', views.ResultsView.as_view(), name='results'),
```

/members/views.py
```py
from django.views import generic

# def index(request):
# def detail(request, question_id):
# def results(request, question_id):

class IndexView(generic.ListView):
    template_name = 'members/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by('-pub_date')[:5]

class DetailView(generic.DeleteView):
    template_name = 'members/detail.html'
    model = Question

class ResultsView(generic.DetailView):
    template_name = 'members/results.html'
    model = Question

```

[generic view 예시](https://docs.djangoproject.com/ko/2.1/ref/class-based-views/generic-display/#listview)

## Members make test bug
/members/tests.py
```py
import datetime
from django.utils import timezone
from .models import Question

class QuestionModelTests(TestCase):
    def test_was_published_recently_with_future_question(self):
        """
        was_published_recently() returns False for questions whose pub_date
        in in the future
        """
        time = timezone.now() + datetime.timedelta(days=30)
        future_question = Question(pub_date=time)
        self.assertIs(future_question.was_published_recently(), False)

```

실행
```sh
python manage.py test members
```

## Members fixup was_published_recently
/members/models.py
```diff
- return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
+ now = timezone.now()
+ return now - datetime.timedelta(days=1) <= self.pub_date <= now
```

실행
```sh
python manage.py test members
```

## Members test more
/members/tests.py
```py
    def test_was_published_recently_with_old_question(self):
        """
        was_published_recently() returns False for questions whose pub_date
        is older tahn 1 day.
        """
        time = timezone.now() - datetime.timedelta(days=1, seconds=1)
        old_question = Question(pub_date=time)
        self.assertIs(old_question.was_published_recently(), False)

    def test_was_published_recently_with_recent_question(self):
        """
        was_published_recently() returns True for questions whose pub_date
        is within the last day.
        """
        time = timezone.now() - datetime.timedelta(hours=23, minutes=59, seconds=59)
        recent_question = Question(pub_date=time)
        self.assertIs(recent_question.was_published_recently(), True)

```

실행
```sh
python manage.py test members
```

## Members view 개선시키기
/members/views.py
```py
from django.utils import timezone

class IndexView(generic.ListView):
    # ...
    def get_queryset(self):
        """
        Return the last five published questions (not including those set to be
        published in the future).
        """
        return Question.objects.filter(pub_date__lte=timezone.now()).order_by('-pub_date')[:5]
            # __lte = 같거나 작다

class DetailView(generic.DetailView):
    # ...
    def get_queryset(self):
        """
        Excludes any questions that aren't published yet.
        """
        return Question.objects.filter(pub_date__lte=timezone.now())

```

[__lte 또는 다른 조건 키워드](http://brownbears.tistory.com/63)

/members/tests.py
```py
from django.urls import reverse

def create_question(question_text, days):
    """
    Create a question with the given `question_text` and published the
    given number of `days` offset to now (negative for questions published
    in the past, positive for questions that have yet to be published).
    """
    time = timezone.now() + datetime.timedelta(days=days)
    return Question.objects.create(question_text=question_text, pub_date=time)

class QuestionIndexViewTests(TestCase):
    def test_no_questions(self):
        """
        If no questions exist, an appropriate message is displayed.
        """
        response = self.client.get(reverse('members:index'))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, "No members are available.")
        self.assertQuerysetEqual(response.context['latest_question_list'], [])

    def test_past_question(self):
        """
        Questions with a pub_date in the past are displayed on the
        index page.
        """
        create_question(question_text="Past question.", days=-30)
        response = self.client.get(reverse('members:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            ['<Question: Past question.>']
        )

    def test_future_question(self):
        """
        Questions with a pub_date in the future aren't displayed on
        the index page.
        """
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse('members:index'))
        self.assertContains(response, "No members are available.")
        self.assertQuerysetEqual(response.context['latest_question_list'], [])

    def test_future_question_and_past_question(self):
        """
        Even if both past and future questions exist, only past questions
        are displayed.
        """
        create_question(question_text="Past question.", days=-30)
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse('members:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            ['<Question: Past question.>']
        )

    def test_two_past_questions(self):
        """
        The questions index page may display multiple questions.
        """
        create_question(question_text="Past question 1.", days=-30)
        create_question(question_text="Past question 2.", days=-5)
        response = self.client.get(reverse('members:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            ['<Question: Past question 2.>', '<Question: Past question 1.>']
        )

class QuestionDetailViewTests(TestCase):
    def test_future_question(self):
        """
        The detail view of a question with a pub_date in the future
        returns a 404 not found.
        """
        future_question = create_question(question_text='Future question.', days=5)
        url = reverse('members:detail', args=(future_question.id,))
        response = self.client.get(url)
        self.assertEqual(response.status_code, 404)

    def test_past_question(self):
        """
        The detail view of a question with a pub_date in the past
        displays the question's text.
        """
        past_question = create_question(question_text='Past Question.', days=-5)
        url = reverse('members:detail', args=(past_question.id,))
        response = self.client.get(url)
        self.assertContains(response, past_question.question_text)

```

## Members static assetes
/members/templates/members/index.html
```py
{% load static %}
<link rel="stylesheet" type="text/css" href="{% static 'members/style.css' %}">
```

/members/static/members/style.css
```css
body {
    background: white url("images/background.gif") no-repeat;
}
/* 이미지 파일 /members/static/members/images/background.gif */
li a {
    color: green;
}

```

재시작 하고 확인

## Members Admin fields order change
/members/admin.py
```py
class QuestionAdmin(admin.ModelAdmin):
    fields = ['pub_date', 'question_text']

```
```diff
- admin.site.register(Question)
+ admin.site.register(Question, QuestionAdmin)
```

Admin Question 확인

```py
class QuestionAdmin(admin.ModelAdmin):
    # fields = ['pub_date', 'question_text']
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]

```

Admin Question 확인

## Members Admin register Choice
```diff
- from .models import Question
+ from .models import Choice, Question

admin.site.register(Choice)

```

## Members Admin Question에서 Choice 등록 하기
/members/admin.py
```py
# class ChoiceInline(admin.StackedInline):
class ChoiceInline(admin.TabularInline):
    model = Choice
    extra = 3

class QuestionAdmin(admin.ModelAdmin):
    # ...
    inlines = [ChoiceInline]
```
```diff
- admin.site.register(Choice)
```

## Members Admin Question change list
/members/admin.py
```py
class QuestionAdmin(admin.ModelAdmin):
    # ...
    list_display = ('question_text', 'pub_date', 'was_published_recently')
    list_filter = ['pub_date']
    search_fields = ['question_text']
```

/members/models.py
```py
class Question(models.Model):
    # ...
    was_published_recently.admin_order_field = 'pub_date'
    was_published_recently.boolean = True
    was_published_recently.short_description = 'Published recently?'
```

## Admin change template path
/django_study/settings.py
```diff
TEMPLATES = [
    {
-        'DIRS': [],
+        'DIRS': [os.path.join(BASE_DIR, 'templates')],

```

Django 소스 파일 경로 찾기
```sh
python -c "import django; print(django.__path__)"
```

Django Admin 소스 파일 경로 이동
```sh
cd {해당경로}/contrib/admin/templates/admin
open .
```

/templates/admin 폴더 생성 후 복사하기

/templates/admin/base_site.html
```html
<!-- <h1 id="site-name"><a href="{% url 'admin:index' %}">{{ site_header|default:_('Semin administration') }}</a></h1> -->
<h1 id="site-name"><a href="{% url 'admin:index' %}">Semin admin</a></h1>
```
