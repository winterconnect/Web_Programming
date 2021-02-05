# Django



# CHAPTER3 Django 웹 프레임워크

> 장고의 애플리케이션 개발 방식과 원리 설명



## 3.1 일반적인 특징

__MVC 패턴 기반 MVT(Model View Template)__

- M(MODEL): 데이터 관점에서 조회, 저장 등 DB 모델링
- V(VIEW): UI, 프로트엔드
- C(CONTROLLER):  백엔드



- 장고에서는 VIEW가 백엔드, TEMPLATE이 프론트엔드



__객체 관계 매핑__

- db.things.save()



__자동으로 구성되는 관리자 화면__



__우아한 URL 설계__



__자체 템플릿 시스템__

- 디자인과 로직에 대한 코딩을 분리하여 독립적으로 개발 진행



__캐시 시스템__



__다국어 지원__



__풍부한 개발 환경__



__소스 변경사항 자동 반영__





## 3.3 장고에서의 애플리케이션 개발 방식

>  전체 프로그램을 __프로젝트 Project__ 라고 하고, 모듈화된 단위 프로그램을 __애플리케이션 Application__ 이라 부른다



### 3.3.1 MVT 패턴

### 3.3.2 Model - 데이터베이스 정의

- __ORM 기법(Object-Relational Mapping)__: 객체와 관계형 데이터베이스를 연결
- 애플리케이션에서 사용할 데이터베이스를 클래스로 매핑해서 코딩
- 모델 클래스는 models.py 파일에 정의



### 3.3.3 URLconf - URL 정의

- 클라이언트로 요청을 받으면 요청이 들어있는 URL을 분석
- urls.py파일에 URL 과 처리함수(view)를 맵핑하는 파이썬 코드를 작성



### 3.3.4 View - 로직 정의

- 웹 요청을 받아서 해당 애플리케이션의 로직에 맞는 처리를 하고(데이터베이스 접속 등)
- 그 결과 데이터를 HTML로 변환하기 위해 템플릿 처리를 한 후,
- 최종 HTML로 된 응답데이터를 웹 클라이언트로 반환하는 역할



- 뷰는 함수 또는 클래스의 메소드로 작성되며, 웹 요청을 받고 응답을 반환함

- 보통 views.py 파일에 작성



### 3.3.5 Template - 화면 UI 정의

- settings.py 파일에 정의되어 있음
- 

### 3.3.6 MVT 코딩 순서

> 모델, 뷰, 템플릿 셋 중 무엇을 먼저 코딩해야하는 지에 대해 정해진 순서는 없음
>
> 화면 설계: 뷰와 템플릿 코딩으로 연결
>
> 테이블 설계: 모델 코딩에 반영

따라서 독립적으로 개발할 수 있는 모델를 먼저 코딩, 

뷰와 템플릿은 서로 영향을 미치므로 모델 이후에 같이 코딩하는 것이 일반적



__순서__

- 프로젝트 뼈대 만들기: 프로젝트 및 앱 개발에 필요한 디렉토리와 파일 생성
- 모델 코딩하기: 테이블 관련 사항을 개발(models.py, admin.py)
- URLconf 코딩하기: URL 및 뷰 매핑 관계를 정의(urls.py)
- 템플릿 코딩하기: 화면 UI  개발(templates/*.html)
- 뷰 코딩하기: 애플리케이션 로직 개발(views.py)





## 실습: 프로젝트 & 애플리케이션 개발



## 3.4 애플리케이션 설계하기

1. 프로젝트란? 개발 대상이 되는 전체 프로그램을 의미

2. 애플리케이션이란? 프로젝트 하위의 서브 프로그램



서브 프로그램인 애플리케이션을 개발하고, 이들을 모아서 프로젝트 개발을 완성!



>  __*개발할 애플리케이션*__
>
> - 설문에 해당하는 질문을 보여준 후, 질문에 포함되어 있는 답변 항목에 투표하면 결과를 알려주는 예제
> - 3개의 페이지를 기준으로 개발한다고 가정
>   - index.html:  질문 리스트
>   - detail.html: 질문에 대한 답변 항목
>   - results.html: 질문에 따른 투표 결과
> - 테이블: Question(질문 저장 테이블), Choice(답변 저장 테이블)





## 3.5 프로젝트 뼈대 만들기

- 프로젝트에 필요한 디렉토리 및 파일을 구성, 설정파일 셋팅
- 기본테이블 생성
- 슈퍼유저(관리자 계정) 생성
- 프로젝트 생성 후 애플리케이션 디렉토리 및 파일 구성



### 3.5.1 프로젝트 생성

```
django-admin startproject mysite
mv mysite ch3
```



### 3.5.2 애플리케이션 생성

```
python3 manage.py startapp polls // polls 라는 애플리케이션 생성
```

- admin
- apps
- models
- views
- tests
- migration/



### 3.5.3 프로젝트 설정 파일 변경

notepad settings.py: 설정파일을 확인 및 수정

- settings.py: 프로젝트의 전반적인 사항들을 설정해주는 곳

```python
 #  True면 개발모드, False면 운영모드
DEBUG = True

# runserver 기동할 서버 IP
ALLOWED_HOSTS = [ 'localhost' , '127.0.0.1' ] 

# Application definition
# 생성한 polls 애플리케이션의 apps.py 파일의 PollsConfig 클래스를 프로젝트 애플리케이션에 등록
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls.apps.PollsConfig', # 추가
]

# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases
# 기본 SQLite3 데이터베이스 엔진을 사용하도록 설정 

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Internationalization
# https://docs.djangoproject.com/en/3.1/topics/i18n/
# 타임존 변경

LANGUAGE_CODE = 'en-us'
# TIME_ZONE = 'UTC'
TIME_ZONE = 'Asia/Seoul'
USE_I18N = True
USE_L10N = True
USE_TZ = True
```



### 3.5.4 기본 테이블 생성

데이터베이스에 기본 테이블을 생성

```
python3 manage.py migrate 
```

- 장고는 모든 웹 프로젝트 개발 시 반드시 사용자와 그룹 테이블이 필요하다는 가정 하에 설계
- 따라서 테이블을 만들지 않았더라도 사용자 및 그룹 테이블 등을 만들어주기 위해 프로젝트 개발 시작 시점에 이 명령을 실행
- 실행 결과로 SQLite3 데이터베이스 파일인 db.sqlite3 파일이 생성됨





### 3.5.5 지금까지 작업 확인하기

현재까지 작업을 개발용 웹 서버로 확인

```
python3 manage.py runserver 0:8000
```



1. http://localhost:8000 으로 접속

2. http://localhost:8000/admin 으로 접속
3. 슈퍼유저 생성

```
python3 manage.py createsuperuser
```

```
winter@Winterui-MacBookPro practice % tree /F ch3
/F [error opening dir]
ch3
├── db.sqlite3
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-39.pyc
│   │   ├── settings.cpython-39.pyc
│   │   ├── urls.cpython-39.pyc
│   │   └── wsgi.cpython-39.pyc
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── polls
    ├── __init__.py
    ├── __pycache__
    │   ├── __init__.cpython-39.pyc
    │   ├── admin.cpython-39.pyc
    │   ├── apps.cpython-39.pyc
    │   └── models.cpython-39.pyc
    ├── admin.py
    ├── apps.py
    ├── migrations
    │   ├── __init__.py
    │   └── __pycache__
    │       └── __init__.cpython-39.pyc
    ├── models.py
    ├── tests.py
    └── views.py

6 directories, 23 files
```



## 3.6 애플리케이션 개발하기 - Model 코딩

- 모델작업: 데이터베이스에 테이블을 생성하는 작업

> 1. notepad models.py
> 2. notepad admins.py
> 3. python3 manage.py makemigrations
> 4. python3 manage.py migrate
> 5. python3 manage.py runserver



### 3.6.1 테이블 정의

- polls 애플리케이션: Question, Choice 두개의 테이블 필요
- 테이블은 models.py 파일에 정의

```python
# models.py

from django.db import models

# Create your models here.

from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length = 200)
    pub_date = models.DateTimeField('date published')
    
    def __str__(self):
        return self.question_text
    
class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete = models.CASCADE)
    choice_text = models.CharField(max_length = 200)
    votes = models.IntegerField(default = 0)
    
    def __str__(self):
        return self.choice_text
```

- 장고에서는 테이블을 하나의 클래스로 정의, 테이블의 컬럼은 클래스의 변수(속성)로 매핑함
- 테이블 클래스는 django.db.models.Model 클래스를 상속받아 정의
- 각 클래스 변수의 타입도 장고에서 미리 정의된 필드 클래스를 사용



### 3.6.2 Admin 사이트에 테이블 반영

- models.py 파일에서 정의한 테이블이 Admin 사이트 화면에 보이게 함

- admins.py 파일에 등록해주면 됨

```python
# admin.py

from django.contrib import admin
from polls.models import Question, Choice 
# models.py 모듈에서 정의한 Question, Choice 클래스를 임포트

# admin.site.register() 함수를 이용하여 임포트한 클래스를 Admin 사이트에 등록
admin.site.register(Question)
admin.site.register(Choice)
```

- 테이블을 새로 만들 때는 models.py, admin.py 두 개의 파일을 함께 수정해야함!



### 3.6.3 데이터베이스 변경사항 반영

```
python3 manage.py makemigrations   # 데이터베이스에 변경이 필요한 사항을 추출함
python3 manage.py migrate  				# 데이터베이스에 변경사항을 반영함
```

- migration
  - 테이블 및 필드의 생성, 삭제, 병경 등과 같은 데이터베이스에 대한 변경사항을 알려주는 정보
  - 애플리케이션 디렉토리별로 migration 파일이 존재
  - makemigrations 명령에 의해 polls/migrations 디렉토리 하위에 마이그레이션 파일들이 생김
  - 이 마이그레이션 파일들을 이용해 migrate 명령으로 데이터베이스에 테이블을 만들어줌



- models.py 모듈에 정의한 테이블을 migrate 명령으로 데이터베이스에 반영할 때, 장고가 사용하는 SQL 문장 확인

```
winter@Winterui-MacBookPro ch3 % python3 manage.py sqlmigrate polls 0001
```

```
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question_text" varchar(200) NOT NULL, "pub_date" datetime NOT NULL);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "question_id" integer NOT NULL REFERENCES "polls_question" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");
COMMIT;
```





### 3.6.4 지금까지 작업 확인하기

현재까지 작업을 개발용 웹 서버로 확인함

```
python3 manage.py runserver
```





## 3.7 애플리케이션 개발하기 - View 및 Template 코딩

- polls 애플리케이션의 3개의 페이지를 보여주기 위해 필요한 뷰와 템플릿을 코딩

- 요청에서 응답까지의 처리흐름에 대한 로직 설계: 4개의 URL과 뷰가 필요하다고 판단

- URL과 뷰는 1:1 관계로 매핑됨 (N:1도 가능)
- URLconf: URL/뷰 매핑을 의미
- urls.py 파일에 작성



>__순서__
>
>- urls.py 작성
>- views.index() 함수 작성
>- views.detail() 함수 작성
>- views.vote() 함수 작성
>- views.results() 함수 작성



### 3.7.1 URLconf 코딩

__mysite/urls.py 파일 코딩__

```python
# urls.py

from django.contrib import admin
from django.urls import path
from polls import views


# URL/뷰 매핑 정의
# URL 패턴 매칭은 위에서 아래로 진행하므로 순서에 유의
urlpatterns = [
    path('admin/', admin.site.urls), # 장고의 Admin 사이트에 대한 URLconf는 이미 정의되어 있음
    path('polls/', views.index, name='index'),
    path('polls/<int:question_id>/', views.detail, name='detail'),
    path('polls/<int:question_id>/results/', views.results, name='results'),
    path('polls/<int:question_id>/vote/', views.vote, name='vote'),
]
```



- mysite/settings.py 파일에 ROOT_URLCONF 항목이 정의되어 있음

```python
# settings.py

ROOT_URLCONF = 'mysite.urls'
```





__mysite/urls.py 와 polls/urls.py 두가지 파일로 작성__

- 더 좋은 방법임!
  - URLconf 모듈을 계층적으로 구성 - 변경과 확장 용이해짐
  - 재사용이 용이해짐

```python
# mysite/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('polls/', include('polls.urls')),
]
```



```python
# polls/urls.py

from django.urls import path
from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'),
    path('<int:question_id>/results/', views.results, name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'), # vote 버튼을 누르면 vote() 뷰 함수가 호출됨
]
```



### 3.7.2 뷰 함수 index() 및 템플릿 작성

- 화면에 질문을 보여주는 로직을 구현하기 위해 뷰 함수와 템플릿 파일을 각각 코딩
- 뷰 함수와 템플릿은 서로 영향을 미치므로 보통 같이 작업
- UI 화면을 생각하면서 로직을 풀어나가는 것이 쉽기 때문에 템플릿을 먼저 코딩하는 것을 추천



__템플릿 작성__

```html
<!--polls/templates/polls/index.html-->

{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href = "/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```



__views.index() 함수 작성__

- 최종적으로 클라이언트에게 응답할 데이터인 HttpResponse 객체를 반환

```python
# polls/views.py

from django.shortcuts import render
from polls.models import Question

def index(request):
    latest_question_list = Question.objects.all().order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```





### 3.7.3 뷰 함수 detail() 및 폼 템플릿 작성

- 템플릿 작성: detail.html

```html
<h1>{{ question.question_text }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'polls:vote' question.id %}" method = "post">
{% csrf_token %}
{% for choice in question.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}" />
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br />
{% endfor %}
<input type="submit" value="Vote" />
</form>
```



- views.py에 detail() 함수 작성

```python
# views.py 

from django.shortcuts import get_object_or_404, render
from polls.models import Question

def index(request):
    latest_question_list = Question.objects.all().order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)

def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```



### 3.7.4 뷰 함수 vote() 및 리다이렉션 작성

- views.py에 vote() 뷰 함수 작성 

```python
from django.shortcuts import get_object_or_404, render
from django.http import HttpResponseRedirect
from django.urls import reverse
from polls.models import Choice, Question

def index(request):
    latest_question_list = Question.objects.all().order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)

def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})

def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        #설문 투표 폼을 다시 보여준다
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        
        # POST 데이터를 정상적으로 처리하였으면,
        # 항상 HttpResponseRedirect를 반환하여 리다이렉션 처리함
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```



__reverse() 함수__

- URL패턴명으로 URL스트링을 구할 수 있음

- URLconf에 이미 정의된 URL 패턴을 활용해서 URL 스트링을 추출하는 방식이므로, 소스에 URL 스트링을 하드코딩하지 않도록 해줌





### 3.7.5 뷰 함수 results() 및 템플릿 작성

- results.html 입력

```html
<h1>{{ question.question_text}}</h1>

<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
{% endfor %}
</ul>

<a href="{% url 'polls:detail' question.id %}">Vote again?</a>
```



### 3.7.6 지금까지 작업 확인하기



-----

- 서버가 request 를 받으면 데이터베이스를 관리하는 어플리케이션이 정보를 조회한 후 html로 전송

- 웹 서버, 데이터베이스 서버를 분리함(과부하 방지)

- 웹프로그램을 한다는 것은? 웹서버 개발

  1. 사이트 설계

  2. 사이트 설계를 토대로 데이터베이스 설계
  3. 인터페이스 설계

- 장고와 같은 웹 프레임워크를 사용하여 웹 서버 개발







- 데이터베이스에 바로 접속할 수 없다

  ex) 공공기관(주민센터)에서 공공 데이터베이스에 접속한다면, 바로 db에 접속하는 것이 아니라 인터페이스로 접속

  인터페이스에 맞춰 정보들을 담아 주민센터로 접속

  인터페이스의 순서는 규약으로 정해져있음 (주민센터-데이터베이스 간)

- 어플리케이션에서는 __API(Application Interface)__, 웹에서는 __CGI (Common Gateway Interface)__



- request: header 파일: 각종 정보를 넣어 전송
- response header 파일



