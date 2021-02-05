# CHAPTER4. Django의 핵심 기능

> 실제 프로젝트 개발을 위해 꼭 알야아할 기능 6가지 설명



## 4.1 Admin 사이트 꾸미기

> Admin
>
> - 데이터베이스에 들어있는 데이터를 쉽게 관리할 수 있도록 데이터의 CRUD(생성, 조회, 변경, 삭제) 등의 기능 제공
> - 깔끔한 UI 제공



### 4.1.1 데이터 입력 및 수정



### 4.1.2 필드 순서 변경하기

polls/admin.py 파일 변경

```python
# admin.py

from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice

# ModelAdmin 클래스를 상속받아 새로운 QuestionAdmin 클래스 정의
class QuestionAdmin(admin.ModelAdmin): 
    fields = ['pub_date', 'question_text'] # 필드 순서 변경

# admin.site.register() 함수의 두번째 인자로 QuestionAdmin 클래스 정의    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```





### 4.1.3 각 필드를 분리해서 보여주기

```python
# admin.py

from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        ('Question Statement', {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date']}),
    ]
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```



### 4.1.4 필드 접기

- admin.py 에 collapse 추가

```python
# admin.py

from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        ('Question Statement', {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}), # collapse 추가
    ]
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```



### 4.1.5 외래키 관계 화면



### 4.1.6 Question 및 Choice를 한 화면에서 변경하기

```python
# admin.py

from django.contrib import admin
from django.contrib import admin
from polls.models import Question, Choice

class ChoiceInline(admin.StackedInline):
    model = Choice
    extra = 2 # 한번에 보여주는 Choice text의 숫자가 결정
    
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline] # Choice 모델 클래스 같이보기
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```



### 4.1.7 테이블 형식으로 보여주기

- TarbularInline 으로 변경

```python
# admin.py

from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice

    
class ChoiceInline(admin.TabularInline):
    model = Choice
    extra = 2
    
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline] # Choice 모델 클래스 같이보기
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```





### 4.1.8 레코드 리스트 컬럼 지정하기

- admin.py 에 list_display 추가

```python
from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice

    
class ChoiceInline(admin.TabularInline):
    model = Choice
    extra = 2
    
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline] # Choice 모델 클래스 같이보기
    list_display = ('question_text', 'pub_date') # 레코드 리스트 컬럼 지정
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```



### 4.1.9 list_filter 필터

- UI 화면 우측에 필터 사이드바 추가
- 사용된 기준 필드 타입에 따라 장고가 자동으로 적절한 항목들을 보여줌



### 4.1.10 search_fields

- UI 화면에 검색박스 표시

```python
# admin.py

from django.contrib import admin

# Register your models here.


from django.contrib import admin
from polls.models import Question, Choice

    
class ChoiceInline(admin.TabularInline):
    model = Choice
    extra = 2
    
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline] # Choice 모델 클래스 같이보기
    list_display = ('question_text', 'pub_date') # 레코드 리스트 컬럼 지정
    list_filter = ['pub_date']
    search_fields = ['question_text'] # 검색박스 추가 
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```



### 4.1.11 polls/admin.py 변경 내역 정리(최종)

```python
from django.contrib import admin
from django.contrib import admin
from polls.models import Question, Choice
    
class ChoiceInline(admin.TabularInline):
    model = Choice
    extra = 2
    
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None, {'fields': ['question_text']}),
        ('Date Information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline] # Choice 모델 클래스 같이보기
    list_display = ('question_text', 'pub_date') # 레코드 리스트 컬럼 지정
    list_filter = ['pub_date'] # 필터 사이드바 추가
    search_fields = ['question_text'] # 검색박스 추가 
    
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```





### 4.1.12 Admin 사이트 템플릿 수정







## 4.2 장고 파이썬 쉘로 데이터 조작하기

### 4.2.1 Create - 데이터 생성/입력



### 4.2.2 Read - 데이터 조회

Question.objects.all()



### 4.2.3 Update - 데이터 수정



### 4.2.4 Delete - 데이터 삭제

Question.objects.delete()



### 4.2.5 polls 애플리케이션의 데이터 실습





## 4.3 템플릿 시스템



### 4.3.1 템플릿 변수

{{ variable }}



### 4.3.2 템플릿 필터

{{ name|lower }} : name 변수값의 모든 문자를 소문자로 바꿔주는 필터

{{ text|escape|linebreaks }} : text변수값 중에 특수문자를 이스케이프해주고 그 결과 스트링에 HTML <p> 태그를 붙임

{{ bio|truncatewords:30 }}

{{ list|join:" // " }}

{{ value|default:"nothing" }}

{{ value|length }}

{{ value|striptags }}

{{ value|pluralize }}





### 4.3.3 템플릿 태그

{% for %} 태그

```
<ul>
{% for athlete in athlete_list %}
	<li>{{ athlete.name }}</li>
{% endfor %}
</ul>
```



{% if %} 태그

```
{% if athlete_list %}
	Number of athletes: {{ athlete_list|length }}
{% elif athlete_in_locker_room_list %}
	Athletes should be out of the locker room soon!
{% else %}
	No athletes.
{% endif %}
```



{% csrf_token %} 태그



{% url %}



{% with %}



{% load %}



### 4.3.4 템플릿 주석

{# #} 한줄주석

{% comment %} 여러줄 주석



### 4.3.5 HTML 이스케이프

< (less than) : &lt

\> (greater than) : &gt



### 4.3.6 템플릿 상속

- 템플릿 상속을 통해 템플릿 코드를 재사용할 수 있고, 사이트의 룩앤필을 일관성 있게 보여줄 수 있음
- 부모템플릿: 템플릿의 뼈대를 만들어주고, {% block %} 태그를 통해 하위로 상속해줄 부분을 지정





## 4.4 폼 처리하기



### 4.4.1 HTML 에서의 폼



### 4.4.2 장고의 폼 기능



### 4.4.3 폼 클래스로 폼 생성



### 4.4.4 뷰에서 폼 클래스 처리



### 4.4.5 폼 클래스를 템플릿으로 변환

{{ form.as_table }} : \<tr> 태그로 감싸서 테이블 셀로 렌더링

{{ form.as_p }} : \<p> 태그로 감싸도록 렌더링

{{ form.as_ul }} : \<li> 태그로 감싸도록 렌더링





## 4.5 클래스형 뷰



### 4.5.1 클래스형 뷰의 시작점



### 4.5.2 클래스형 뷰의 장점

- 효율적인 메소드 구분
- 상속 기능 가능



### 4.5.4 클래스형 제네릭 뷰



### 4.5.5 클래스형 뷰에서 폼 처리





## 4.6 로그 남기기

### 4.6.1 로거(Logger)

- 로깅시스템의 시작점으로 로그 메세지를 처리하기 위해 메세지를 담아두는 저장소
- 로그 레벨: 로그 메세지의 중요도에 따라 자신이 어느 레벨 이상의 메세지를 처리할지에 대한 기준이 됨

| 로그 레벨 | 정수값 | 설명                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| NOTSET    | 0      | 로그 레벨의 최하위 수준<br />로거 또는 핸들러가 생성될 때도 별도 설정이 없으면 갖는 디폴트 로그 레벨 |
| DEBUG     | 10     | 디버그 용도로 사용되는 정보                                  |



### 4.6.2 핸들러

- 로거에 있는 메세지에 무슨 작업을 할지 결정하는 엔진

  

### 4.6.3 필터

- 로그 레코드가 로거에서 핸들러로 넘겨질 때, 필터를 사용해서 로그 레코드에 추가적인 제어

  

### 4.6.4 포맷터

- 로그 레코드는 최종적으로 텍스트로 표현되는데, 포멧터는 텍스트로 표현 시 사용할 포멧을 지정해줌



### 4.6.5 로거 사용 및 로거 이름 계층화



### 4.6.6 장고의 디폴트 로깅 설정



### 4.6.7 장고의 로깅 추가 사항 정리



### 4.6.8 로깅 설정

#### 디폴트 설정 유지

#### 디폴트 설정 무시



