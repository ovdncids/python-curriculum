# Session7
## model 만들기
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

todos/templates/home.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do-List 게시판</title>
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
                <td>{{todo.title}}</td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
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

todos/views.py
```py
from django.shortcuts import render
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
```
