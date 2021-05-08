# Session7
## Todo 만들기
todos/models.py
```py
from django.db import models

class Todo(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    deadline = models.DateField()

    def __str__(self):
        return self.title
```

todos/views.py
```py
from django.shortcuts import render, redirect
from .models import Todo
from datetime import datetime

def home(request):
    todos = Todo.objects.all()
    return render(request, 'home.html', {'todos': todos})

def new(request):
    if request.method == 'POST':
        formattedDate = datetime.now().strftime("%Y-%m-%d")
        Todo.objects.create(
            title = request.POST['title'],
            content = request.POST['content'],
            deadline = request.POST['deadline'] or formattedDate,
        )
    return render(request, 'new.html')

def detail(request, todo_pk):
    todo = Todo.objects.get(pk=todo_pk)
    return render(request, 'detail.html', {'todo': todo})

def edit(request, todo_pk):
    todo = Todo.objects.get(pk=todo_pk)
    if request.method == 'POST':
        formattedDate = datetime.now().strftime("%Y-%m-%d")
        Todo.objects.filter(pk=todo_pk).update(
            title = request.POST['title'],
            content = request.POST['content'],
            deadline = request.POST['deadline'] or formattedDate,
        )
        return redirect('detail', todo_pk)
    return render(request, 'edit.html', {'todo': todo})

def delete(request, todo_pk):
    todo = Todo.objects.get(pk=todo_pk)
    todo.delete()
    return redirect('home')
```

todos/templates/home.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do-List 게시판</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <h1>To-Do-List Home</h1>
    <table>
        <thead>
            <tr>
                <th>제목</th>
            </tr>
        </thead>
        <tbody>
            {% for todo in todos %}
            <tr>
                <td><a href="{% url 'detail' todo.pk %}">{{todo.title}}</a></td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
    <a href="{% url 'new' %}">글 쓰러가기</a>
</body>
</html>
```

todos/templates/new.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do-List 게시판</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <h1>To-Do-List Create</h1>
    <form action="" method="post">
        {%	csrf_token %}
        <table>
            <tbody>
                <tr>
                    <th>제목</th>
                    <td><input type="text" name="title" placeholder="제목을 입력해주세요."></td>
                </tr>
                <tr>
                    <th>내용</th>
                    <td><textarea name="content" cols="30" rows="10" placeholder="내용을 입력해주세요."></textarea></td>
                </tr>
                <tr>
                    <th>마감일</th>
                    <td><input type="date" name="deadline"></td>
                </tr>
            </tbody>
        </table>
        <button type="submit">작성하기</button>
    </form>
</body>
</html>
```

todos/templates/detail.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do-List 게시판</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <h1>To-Do-List Read</h1>
    <table>
        <tbody>
            <tr>
                <th>제목</th>
                <td>{{todo.title}}</td>
            </tr>
            <tr>
                <th>내용</th>
                <td>{{todo.content}}</td>
            </tr>
            <tr>
                <th>마감일</th>
                <td>{{todo.deadline | date:'Y-m-d'}}</td>
            </tr>
        </tbody>
    </table>
    <a href="{% url 'home' %}">홈으로</a>
    <a href="{% url 'edit' todo.pk %}">수정하기</a>
    <a href="{% url 'delete' todo.pk %}">삭제하기</a>
</body>
</html>
```


todos/templates/edit.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do-List 게시판</title>
    {% load static %}
    <link href="{% static 'index.css' %}" rel="stylesheet">
</head>
<body>
    <h1>To-Do-List Update</h1>
    <form action="" method="post">
        {%	csrf_token %}
        <table>
            <tbody>
                <tr>
                    <th>제목</th>
                    <td><input type="text" name="title" placeholder="제목을 입력해주세요." value="{{todo.title}}"></td>
                </tr>
                <tr>
                    <th>내용</th>
                    <td><textarea name="content" cols="30" rows="10" placeholder="내용을 입력해주세요.">{{todo.content}}</textarea></td>
                </tr>
                <tr>
                    <th>마감일</th>
                    <td><input type="date" name="deadline" value="{{todo.deadline | date:'Y-m-d'}}"></td>
                </tr>
            </tbody>
        </table>
        <button type="submit">작성하기</button>
    </form>
</body>
</html>
```

## 마감 기한이 적게 남은 순 정렬
todos/views.py
```diff
def home(request):
- todos = Todo.objects.all()
+ todos = Todo.objects.all().order_by('deadline')
```

## 마감 기한으로부터 오늘까지 남은 날짜 계산
todos/views.py
```py
for todo in todos:
    diff_date = todo.deadline - datetime.date(datetime.now())
    todo.remain = diff_date.days
```
