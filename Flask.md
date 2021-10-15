# Flask
* https://flask.palletsprojects.com/en/2.0.x/installation
* https://flask.palletsprojects.com/en/2.0.x/quickstart

## 설치
```sh
pip install Flask
```

## 프로젝트 생성
```sh
mkdir flask-study
cd flask-study
code .
```

## 개발 모드
```sh
# Mac
export FLASK_ENV=development
# Windows
set FLASK_ENV=development
```

## 파일 생성
app.py
```py
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/membersRead')
def members_read():
    return render_template('members.html')
```

templates/members.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Members</title>
    <link href="{{ url_for('static', filename='css/app.css') }}" rel="stylesheet">
</head>
<body>
    <div>
        <header>
            <h1>Flask study</h1>
        </header>
        <hr />
        <div class="container">
            <nav class="nav">
                <ul>
                    <li><h2><a href="/membersRead" class="active">Members</a></h2></li>
                    <li><h2><a href="/search">Search</a></h2></li>
                </ul>
            </nav>
            <hr />
            <section class="contents">
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
                                        <form method="POST">
                                            <button>Update</button>
                                            <button>Delete</button>
                                        </form>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <hr class="d-block" />
                    <div>
                        <h4>Create</h4>
                        <form method="POST" action="/membersCreate">
                            <input type="text" name="name" placeholder="Name" />
                            <input type="text" name="age" placeholder="Age" />
                            <button>Create</button>
                        </form>
                    </div>
                </div>
            </section>
            <hr />
        </div>
        <footer>Copyright</footer>
    </div>
</body>
</html>
```

static/css/app.css
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
h1, footer, .nav ul {
  padding: 0.5rem;
}
h4, li {
  margin: 0.5rem 0;
}
hr {
  display: none;
  margin: 1rem 0;
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

## 서버 실행
```sh
flask run
```
* http://127.0.0.1:5000/membersRead

## 회원(Members) CRUD
### Read
app.py
```py
from typing import List, Optional
from pydantic import BaseModel
from flask import Flask, render_template
app = Flask(__name__)

class Member(BaseModel):
    name: str
    age: Optional[int]

members: List[Member] = []
members.append(Member(name='홍길동', age=39))
members.append(Member(name='김삼순', age=33))
members.append(Member(name='홍명보', age=44))
members.append(Member(name='박지삼', age=22))
members.append(Member(name='권명순', age=10))

@app.route('/membersRead', methods=['GET'])
def members_read():
    return render_template('members.html', members=enumerate(members))
```

templates/members.html
```diff
<tr>
    <td>홍길동</td>
    <td>20</td>
    <td>
        <button>Update</button>
        <button>Delete</button>
    </td>
</tr>
```
```html
{% for index, member in members %}
    <form method="POST">
    <tr>
        <td>{{ member.name }}</td>
        <td>{{ member.age }}</td>
        <td>
            <button>Update</button>
            <button>Delete</button>
        </td>
    </tr>
    </form>
{% endfor%}
```

### Create
app.py
```diff
- from flask import Flask, render_template
+ from flask import Flask, render_template, request
```
```py
@app.route('/membersCreate', methods=['POST'])
def members_create():
    member = Member(
        name = request.form['name'],
        age = request.form['age']
    )
    members.append(member)
    return '<script>document.location.href = "/membersRead";</script>'
```

### Delete
app.py
```py
@app.route('/membersDelete/<int:index>', methods=['POST'])
def members_delete(index):
    del members[index]
    return '<script>document.location.href = "/membersRead";</script>'
```

templates/members.html
```diff
- <button>Delete</button>
```
```html
<button onclick="this.form.action = '/membersDelete/{{index}}';">Delete</button>
```

### Update
app.py
```py
@app.route('/membersUpdate/<int:index>', methods=['POST'])
def members_update(index):
    members[index] = Member(
        name = request.form['name'],
        age = request.form['age']
    )
    return '<script>document.location.href = "/membersRead";</script>'
```

templates/members.html
```diff
- <td>{{ member.name }}</td>
- <td>{{ member.age }}</td>
+ <td><input type="text" name="name" placeholder="Name" value="{{ member.name }}" /></td>
+ <td><input type="text" name="age" placeholder="Age" value="{{ member.age }}" /></td>
```
```diff
- <button>Update</button>
+ <button onclick="this.form.action = '/membersUpdate/{{index}}';">Update</button>
```

## 실행
```sh
flask run
```
