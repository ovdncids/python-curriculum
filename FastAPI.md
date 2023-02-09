# FastAPI
* https://fastapi.tiangolo.com

## 설치
```sh
pip install fastapi
pip install uvicorn[standard]
```

## 프로젝트 생성
```sh
mkdir fastapi-study
cd fastapi-study
code .
```

main.py
```py
from typing import List, Optional
from pydantic import BaseModel
from fastapi import FastAPI

app = FastAPI()

class User(BaseModel):
    name: str
    age: Optional[int]

users: List[User] = []
users.append(User(name='홍길동', age=39))
users.append(User(name='김삼순', age=33))
users.append(User(name='홍명보', age=44))
users.append(User(name='박지삼', age=22))
users.append(User(name='권명순', age=10))

@app.get('/api/v1/users')
def users_read():
# def users_read(name: Optional[str] = Query(None), age: Optional[int] = Query(None)):
    return {
        'result': 'read',
        'users': users
    }

@app.post('/api/v1/users')
def users_create(user: User):
    users.append(user)
    return {'result': 'created'}

@app.delete('/api/v1/users/{index}')
def users_delete(index: int):
    del users[index]
    return {'result': 'deleted'}

@app.patch('/api/v1/users/{index}')
def users_update(index: int, user: User):
    users[index] = user
    return {'result': 'updated'}
```

## 실행
```sh
uvicorn main:app --reload
```

* http://127.0.0.1:8000/docs
* http://127.0.0.1:8000/redoc

### uvicorn 실행이 안 된다면
```sh
pip show uvicorn
  # uvicorn의 설치 정보, 경로등을 볼 수 있다. (Location 정보가 중요)

{Location: 경로/site-packages}../Scripts/uvicorn main:app --reload
```
