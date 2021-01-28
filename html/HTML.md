# HTML

- 가장 기본
- 인터넷으로 데이터를 주고받을 때 사용하는 용어
- 데이터베이스에서 SQL을 쓰는 것처럼 웹페이지에서는 HTML을 쓴다
- 정적인 방법 / 동적인 방법
- 동적인 방법 예: 로그인을 하면 보는 창이 달라짐



- html은 index.html 이라는 메인 페이지에서 시작된다
- 링크로 연결된다
- 인터넷이라는 것은, html 페이지가 묶여 연결되어 있는 것이다!







__\<! >__: 주석



__HTML의 기본구성__

- 구글의 개발자도구를 잘 활용하자

```html
<!DOCTYPE html>

<html>

	<head>
    <title>WEB1 - HTML</title>
  	<meta charset ="UTF-8">
  </head>
  
	<body>
	  <div>
	    <ol>
	      <li>cloud</li>
	      <li>IoT</li>
	      <li>Bigdata</li>
	    </ol>
	  </div>
  </body>
</html>


<table>
  <tr>
	  <td>head</td>
	  <td>98.1%</td>
  </tr>
  <tr>
  	<td>BODY</td>
  	<td>97.9%</td>
  </tr>
</table>
```





__만약 이것을 파이썬으로 구현한다면? (웹크롤링)__

- url request 를 보내고, html 로 response(index.html)를 받음. html 파일을 받아서 필요한 값들이 있는 부분을 확인(찾기 기능 활용)하여 추출함
- 태그를 찾아서 내용을 추출







- HTML만 쓰다보니 여러가지 불편한 점들이 생김(디자인 등)



### HTML의 기본 구성요소

- 태그: < > </ >

- 속성: 태그 안의 성질(font, size 등)



### 1. 태그

> Hypertext Markup Language(HTML) is the standard markup language for creating web pages and web applications



__tag의 시작과 끝__: < > </ >

```html
Hypertext Markup Language(HTML) is the standard markup language for <strong> creating web pages </strong> and web applications.
```



__\<u>__ :underbar

```html
Hypertext Markup Language(HTML) is the standard markup language for <strong> creating <u>web</u> pages </strong> and web applications.
```



__\<html> \</head>__



__\<body> \</body>__



__\<h1> \<h2> ... \<h6>__

```html
<h1> Hello World!! </h1>
<h2> Hello World!! </h2>
<h3> Hello World!! </h3>
```

 

__\<br>__: 줄 나누기

```html
Hypertext Markup Language(HTML) is the standard markup langauge for <strong> creating <u> web </w> pages </strong> and web applications. Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. <br><br> HTML describes the structure of a web page semenatically and originally included cues for the appearance of the document.
```



__\<p> \</p>__: 단락 나누기

```html
<h1>
  HTML
</h1>
<p>
Hypertext Markup Language(HTML) is the standard markup langauge for <strong> creating <u> web </w> pages </strong> and web applications. Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. <p>
  
</p>HTML describes the structure of a web page semenatically and originally included cues for the appearance of the document.
</p>
```



__파라미터값 넣기__

__\<p style="margin-top:40px;">__

```html
<h1>
  HTML
</h1>
<p>
  Hypertext Markup Language(HTML) is the standard markup langauge for <strong> creating <u> web </w> pages </strong> and web applications. Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. </p>
  
<p style = "margin-top:40px;">HTML describes the structure of a web page semenatically and originally included cues for the appearance of the document.
</p>
```





__\<span style="font-size:24px">__

- \<h2>, \<h3> 등 외에도 세부적인 옵션을 조절 가능 (더 많이 사용하게 됨)

```html
<span style="font-size:24px">
  coding
</span>
```





__\<img src="">__

```html
<img src="coding.jpg" width = "100%">
```



### 목차태그

__\<li> \</li>__:리스트 만들기

```html
<li>1.html</li>
<li>2.CSS</li>
<li>3.JavaScript</li>
```



__리스트의 부모태그(ul, ol)__

__\<ul> \</ul>__: Unordered List 번호 없음

```html
<ul>
  <li>1.HTML</li>
  <li>2. CSS</li>
  <li>3. JavaScript</li>
</ul>
<ul>
  <li>egoing</li>
  <li>k8805</li>
  <li>youbin</li>
</ul>
```



__\<ol> \</ol>__: Ordered List. 번호 생성됨

```html
<ol>HTML</ol>
<ol>CSS</ol>
<ol>JavaScript</ol>

<ol>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ol>
```



__\<tr> \</tr>__



__\<title> \</title>__

```html
<title>WEB1 - HTML</title>

<ol>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ol>
```



__\<link> \</link>__



__\<a> \</a>__

```html
<a href="https：//www.w3.org/TR/html5/" target="_blank">Hypertext Markup Language (HTML)</a>
```





__\<span> \</span>__

- 의미있는 태그는 아니다

```

```



__\<table> \</table>__



## CSS

- HTML 기반, 디자인(색상, 모양, 폰트)을 편하게 하기 위한 __언어__



__CSS를 작성하는 방법 2가지__

1. 속성 style
2. 태그 \<style> \</style>: 언어를 HTML안의 태그로 녹여서 사용하는 것



__CSS를 지배하는 두가지 중요한 토대__

1. 효과
2. 선택자





## Javascript

- HTML 기반, 동적으로 핸들링할 때(이벤트, 액션) 사용하는 언어



__\<script> \</script>__



## Django Framework

- 









### 실습해보기

__링크를 걸어 웹페이지를 만들자__



1. 링크로 연결되도록 하자 (본 파일, 각각의 웹페이지 html 생성)

```html
<html>
    <head>
        <title>WEB1 - HTML</title>
        <meta charset="utf-8">
    </head>
    <body>
        <h1><a href="index.html">WEB</a></h1>
        <ol>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
          <li></li><a href="3.html">JavaScript</a></ol></li>
        </ol>
        <h2>HTML이란 무엇인가?</h2>
        ...생략...
    </body>
</html>
```





