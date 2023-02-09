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

@app.route('/usersRead')
def users_read():
    return render_template('users.html')
```

templates/users.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Users</title>
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
                    <li><h2><a href="/usersRead" class="active">Users</a></h2></li>
                    <li><h2><a href="/search">Search</a></h2></li>
                </ul>
            </nav>
            <hr />
            <section class="contents">
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
                        <form method="POST" action="/usersCreate">
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
* http://127.0.0.1:5000/usersRead

## 회원(Users) CRUD
### Read
app.py
```py
from typing import List, Optional
from pydantic import BaseModel
from flask import Flask, render_template
app = Flask(__name__)

class User(BaseModel):
    name: str
    age: Optional[int]

users: List[User] = []
users.append(User(name='홍길동', age=39))
users.append(User(name='김삼순', age=33))
users.append(User(name='홍명보', age=44))
users.append(User(name='박지삼', age=22))
users.append(User(name='권명순', age=10))

@app.route('/usersRead', methods=['GET'])
def users_read():
    return render_template('users.html', users=enumerate(users))
```

templates/users.html
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
{% for index, user in users %}
    <form method="POST">
    <tr>
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
        <td>
            <button>Update</button>
            <button>Delete</button>
        </td>
    </tr>
    </form>
{% endfor %}
```

### Create
app.py
```diff
- from flask import Flask, render_template
+ from flask import Flask, render_template, request
```
```py
@app.route('/usersCreate', methods=['POST'])
def users_create():
    user = User(
        name=request.form['name'],
        age=request.form['age']
    )
    users.append(user)
    return '<script>document.location.href = "/usersRead";</script>'
```

### Delete
app.py
```py
@app.route('/usersDelete/<int:index>', methods=['POST'])
def users_delete(index):
    del users[index]
    return '<script>document.location.href = "/usersRead";</script>'
```

templates/users.html
```diff
- <button>Delete</button>
```
```html
<button onclick="this.form.action = '/usersDelete/{{index}}';">Delete</button>
```

### Update
app.py
```py
@app.route('/usersUpdate/<int:index>', methods=['POST'])
def users_update(index):
    users[index] = User(
        name=request.form['name'],
        age=request.form['age']
    )
    return '<script>document.location.href = "/usersRead";</script>'
```

templates/users.html
```diff
- <td>{{ user.name }}</td>
- <td>{{ user.age }}</td>
+ <td><input type="text" name="name" placeholder="Name" value="{{ user.name }}" /></td>
+ <td><input type="text" name="age" placeholder="Age" value="{{ user.age }}" /></td>
```
```diff
- <button>Update</button>
+ <button onclick="this.form.action = '/usersUpdate/{{index}}';">Update</button>
```

## 검색(Search) 
### Search 페이지 Markup 적용
templates/search.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Search</title>
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
                    <li><h2><a href="/usersRead">Users</a></h2></li>
                    <li><h2><a href="/search" class="active">Search</a></h2></li>
                </ul>
            </nav>
            <hr />
            <section class="contents">
                <div>
                    <h3>{{result}}</h3>
                    <hr class="d-block" />
                    <div>
                        <form>
                            <input type="text" placeholder="Search" name="q" />
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
                            {% for index, user in users %}
                                <tr>
                                    <td>{{ user.name }}</td>
                                    <td>{{ user.age }}</td>
                                </tr>
                            {% endfor %}
                            </tbody>
                        </table>
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

app.py
```py
@app.route('/search', methods=['GET'])
def search():
    return render_template('search.html', users=enumerate(users), result="Search")
```

### Search 검색 기능 적용
templates/search.html
```diff
- <input type="text" placeholder="Search" name="q" />
+ <input type="text" placeholder="Search" name="q" value="{{q}}" />
```

app.py
```py
@app.route('/search', methods=['GET'])
def search():
    q = request.args.get('q') or ''
    searchUsers = []
    for user in users:
        if not q or (q in user.name):
            searchUsers.append(user)
    return render_template(
        'search.html',
        users=enumerate(searchUsers),
        result="Search",
        q=q
    )
```

## route 파일 나누기
* https://stackoverflow.com/questions/11994325/how-to-divide-flask-app-into-multiple-py-files

routes/search.py
```py
from flask import render_template, request, Blueprint

search_page = Blueprint('search_page', __name__, template_folder='templates')

@search_page.route('/search', methods=['GET'])
def search():
    q = request.args.get('q') or ''
    searchUsers = []
    for user in searchUsers:
        if not q or (q in user.name):
            searchUsers.append(user)
    return render_template(
        'search.html',
        users=enumerate(searchUsers),
        result="Search",
        q=q
    )
```

app.py
```diff
- @app.route('/search', methods=['GET'])
```
```py
from routes.search import search_page

app = Flask(__name__)
app.register_blueprint(search_page)
```
* ❔ `User, users` 부분 `models/users.py` 파일로 빼기
