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

## 카카오 연동 페이지 - 만들기
kakao_app/templates/kakao_app.html
```html
카카오 로그인 페이지
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

### 카카오 개발자 페이지에 앱 생성
* https://developers.kakao.com
```sh
내 애플리케이션 -> 애플리케이션 추가하기 -> 앱 이름: django login test1

생성한 애플리케이션으로 이동
요약 정보 -> REST API 키 (Django에서 Client id로 사용됨)
플랫폼 -> Web 플랫폼 등록 -> http://127.0.0.1:8000
카카오 로그인 -> 활성화 설정 -> 활성화
카카오 로그인 -> Redirect URI -> http://127.0.0.1:8000/accounts/kakao/login/callback/
카카오 로그인, 동의 항목 -> 닉네임 -> 필수 동의 (회원 로그인 목적 입니다.)
카카오 로그인, 보안 -> Client Secret -> 코드 생성 (생성된 코드는 Django에서 Secret key로 사용됨)
```

## Admin 페이지 만들기
```sh
python manage.py migrate
python manage.py createsuperuser
```

* http://127.0.0.1:8000/admin
```sh
SITES -> Sites -> example.com -> Domain name: http://127.0.0.1:8000
SITES -> Sites -> example.com -> Display name: http://127.0.0.1:8000
```
```sh
SOCIAL ACCOUNTS -> Social applications -> Add
    Provider: Kakao
    Name: Kakao
    Client id: 카카오 개발자 페이지의 REST API 키
    Secret key: 카카오 개발자 페이지의 Client Secret 코드
    Sites: http://127.0.0.1:8000 -> Chosen sites으로 이동
    Save
```

## 카카오 연동 페이지 - 로그인 기능
kakao_app/templates/kakao_app.html
```html
{% load socialaccount %}
{% providers_media_js %}

{% if user.is_authenticated %}
안녕하세요, {{ user.username }}님
<a
    href="{% url 'logout' %}"
    onclick="window.open('https://accounts.kakao.com/logout?continue=https://accounts.kakao.com/weblogin/account')"
>(로그아웃)</a>
{% else %}
<a href="{% provider_login_url 'kakao' %}">카카오 로그인</a>
{% endif %}
```

kakao_app/views.py
```py
from django.contrib import auth

def logout(request):
    auth.logout(request)
    return redirect('kakao_app')
```

kakao_login/urls.py
```py
path('logout/', views.logout, name='logout'),
```
