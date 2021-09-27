# 카카오 로그인

## 프로젝트 생성
```sh
django-admin startproject kakao_login
cd kakao_login
code .
```
* `django-curriculum`의 `VSCode debug 모드`까지 동일

## 앱 생성
```sh
python manage.py startapp kakao_app
```

## 카카오 연동 페이지 만들기
kakao_app/templates/kakao_app.html
```html
<form method="post">
    <button>카카오 로그인</button>
</form>
```

kakao_app/views.py
```py
from django.shortcuts import render, redirect

def kakao_app(request):
    return render(request, 'kakao_app.html')

def root(request):
    return redirect('kakao_app/')
```

kakao_login/settings.py
```py
INSTALLED_APPS = [
    'kakao_app',
```

kakao_login/urls.py
```py
from kakao_app import views as views

urlpatterns = [
    path('kakao_app/', views.kakao_app, name='kakao_app'),
    path('', views.root),
```
