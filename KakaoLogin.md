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
    {% csrf_token %}
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

## 카카오 연동 라이브러리 설치
```sh
pipenv install django-allauth
```

kakao_login/settings.py
```py
INSTALLED_APPS = [
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.kakao',
```
```py
# Kakao login 설정
AUTHENTICATION_BACKENDS = ( 
    # 'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)
SITE_ID = 1 
LOGIN_REDIRECT_URL = '/'
```

kakao_login/urls.py
```diff
- from django.urls import path
+ from django.urls import path, include
```
```py
urlpatterns = [
    path('accounts/', include('allauth.urls')),
```
