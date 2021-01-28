# WEB PROGRAMMING

> CHAPTER1 웹 프로그래밍의 이해
>
> ​	1.1 웹 프로그래밍이란?
>
> ​	1.2 다양한 웹 클라이언트
>
> ​	1.3 HTTP 프로토콜
>
> ​	1.4 URL 설계
>
> ​	1.5 웹 애플리케이션 서버
>
> 
>
> CHAPTER2 파이썬 웹 표준 라이브러리





## 네트워크(Network)

- 네트워크는 __규약(protocol)__이다
- "나 이제 공 던질게!" "나 글로브 가져올게!" "던진다!" "잘 받았어!" 처럼 통신을 하기 위해 정해놓은 규칙들
  - 메세지를 어떻게 보내야할지 정해져있음: "패킷"으로 정보 저장
  - 컴퓨터는 비트로 정보 저장 (01010111...)
  - 정보를 저장해두었다 패킷을 통해 정보 전달



- 예전에는 구리선으로 연결된 아날로그(주파수)
- 주파수를 디지털화(주파수에 맞는 데이터를 전송) - 자동으로 아날로그 신호로 변환을 해주는 프로그램이 생겨나게 됨
  - ex) 아날로그(통신언어) -> "01010101"(컴퓨터언어) -> 안녕하세요"(사람언어)
  - "안녕하세요" -> "01010101" -> 아날로그



- 패킷

  - SIP(Source IP): 보내는사람 IP
  - DIP(Destination IP): 받는사람 IP
  - C(Control): 메세지의 용도 표시(송신용send, 수신용, 특별용 등), ftp, http 등을 입력
  - Port: 1~1000 까지의 포트는 규약으로 정해져있음 (ex. http 80, ftp: 21,22)
  - 나머지 칸에 데이터 저장

  -> 양쪽 컴퓨터가 모두 준비가 되면 네트워크 시작

- 송신자가 패킷을 보내려니 너무 크면? 패킷을 자름(sip, dip는 패킷마다 표시하고 데이터는 분할하여 송신)

- 수신자는 분할된 패킷을 보고, 조합하여 하나로 만들어서 다시 사용

- 수신자에게 갈 때까지 패킷들은 각각 다른 스위치(=라우터)를 거치며 경로가 다양하고, 만약 분할된 데이터중 일부가 안오게 되면? 들어올 때까지 대기하게 됨



- 통신의 목적? 정보 교환



- __OSI 7 계층(layer)__





## CHAPTER1. 웹 프로그래밍의 이해

### 1.1 웹 프로그래밍이란?



- 서버가 request 를 받으면 데이터베이스를 관리하는 어플리케이션이 정보를 조회한 후 html로 전송

- 웹 서버, 데이터베이스 서버를 분리함(과부하 방지)

- 웹프로그램을 한다는 것은? 웹서버 개발

  1. 사이트 설계

  2. 사이트 설계를 토대로 데이터베이스 설계
  3. 인터페이스 설계

- 장고와 같은 웹 프레임워크를 사용하여 웹 서버 개발



### 1.2 다양한 웹 클라이언트

#### 1.2.1 웹 브라우저를 사용하여 요청

#### 1.2.2 리눅스 curl 명령어를 사용하여 요청

#### 1.2.3 Telnet을 사용하여 요청

#### 1.2.4 직접 만든 클라이언트로 요청

```python
import urllib.request
print(urllib.request.urlopen("http://www.example.com").read().decode('utf-8'))
```





### 1.3 HTTP 프로토콜

>## 인터넷 (http)
>
>- 통신을 하면서 많은 프로토콜이 생겨나게 됨 (telnet, ftp, http 등...)
>
>  - telnet: 서버에 접속해 메세지를 주고받는 프로토콜
>  - ftp(file transfer protocol): 파일전송 프로토콜
>  - http: 
>
>- http의 규약:  request - response
>
>  
>
>- 인터넷으로 웹에 접속한다는 것은? client(pc) - server(홈페이지): html로 소통함
>
>  - client가 http 프로토콜을 이용해서 데이터를 요청 (request)
>  - server는 반드시 대답해야 함(response): html로 만든 메세지(파일)를 전송
>    - index.html 을 갖고 있음
>    - index: 홈페이지 첫페이지 의미
>  - 서버가 index를 클라이언트에게 보내주고, 클라이언트가 이것을 해독하여 필요한 정보를 가져가고, 태그에 따라 브라우저에 표시
>
>  
>
>  - ex) 클라이언트가 브라우저 페이지를 요청(html로 요청) - 서버가 브라우저의 html을 전송
>  - 브라우저가 html를 해독하여 그 내용을 화면에 그대로 보여줌



#### 1.3.1 HTTP 메시지의 구조

#### 1.3.2 HTTP 처리 방식

- 8가지가 있지만 현실적으로 가장 많이 사용하는 메소드는 GET, POST
- request header에 들어감
  - GET 요청방식: 지정한 url의 정보를 가져오는 메서드(데이터 조회 read)
  - POST 요청방식: 리소스를 생성 (데이터 생성  create)

#### 1.3.3 GET과 POST 메소드

#### 1.3.4 상태 코드



### 1.4 URL 설계

- URL scheme: URL에 사용된 프로토콜 의미
- netloc: 네트워크 위치. http 프로토콜은 host:port 형식으로 표현
  - host: 웹 서버의 호스트명, 도메인명 또는 IP 주소
  - port: 웹 서버 내의 서비스 포트번호. 생략시에 디폴트 포트번호 사용(http 80, https 443)
- path: 파일이나 애플리케이션 경로
- params: 애플리케이션에 전달될 매개변수
- query: 질의 문자열 또는 매개변수. 앰퍼샌드(&)로 구분된 이름-값 쌍 형식으로 표현
- fragment: 문서 내의 앵커 등 조각을 지정



#### 1.4.1 URL을 바라보는 측면

#### 1.4.2 간편 URL

#### 1.4.3 파이썬의 우아한 URL



### 1.5 웹 애플리케이션 서버



#### 1.5.1. 정적페이지 vs 동적페이지

> - 사용자가 페이지를 요청하는 시점에 페이지의 내용이 유지되는가 변경되는가를 구분해주는 용어
>
> - 동적페이지에는 프로그래밍 코드가 포함되어 있어서 페이지 요청시점에 HTML 문장을 만들어내는 것





#### 1.5.3 CGI 방식의 대안기술



#### 1.5.4 애플리케이션 서버 방식

웹클라이언트 - 웹서버 - 웹 애플리케이션 서버



#### 1.5.5 웹서버와의 역할 구분



## CHAPTER2. 파이썬 웹 표준 라이브러리

> 2.1 웹 라이브러리 구성
>
> 2.2 웹 클라이언트 라이브러리
>
> 2.3 웹 서버 라이브러리
>
> 2.4 CGI/WSGI 라이브러리





### 2.1 웹 라이브러리 구성

- 웹 클라이언트 프로그래밍: urllib 패키지(고수준 API 제공)
- 웹 서버 프로그래밍: Web Framework(Django, Flask, Tornado 등)



- urllib 패키지: 웹 클라이언트를 작성하는데 사용되는 모듈들이 있으며, 가장 빈번하게 사용하는 모듈

- http 패키지

  - 서버용과 클라이언트용 라이브러리로 나누어 모듈을 담고 있음
  - 쿠키 관련 라이브러리도 서버용과 클라이언트용 모듈이 구분됨

  

### 2.2 웹 클라이언트 라이브러리

#### 2.2.1 urllib.parse 모듈

- URL의 분해, 조립, 변경 및 URL 문자인코딩, 디코딩 등을 처리하는 함수 제공

```python
from urllib.parse import urlparse
result = urlparse("http://www.python.org:80/guido/python.html;philosophy?overall=3#n10")
result
```

결과: URL 구성요소대로 파싱됨

```
ParseResult(scheme='http', netloc='www.python.org:80', path='/guido/python.html', params='philosophy', query='overall=3', fragment='n10')
```



- __URL scheme__: URL에 사용된 프로토콜 의미
- __netloc__: 네트워크 위치. http 프로토콜은 host:port 형식으로 표현
  - host: 웹 서버의 호스트명, 도메인명 또는 IP 주소
  - port: 웹 서버 내의 서비스 포트번호. 생략시에 디폴트 포트번호 사용(http 80, https 443)
- __path__: 파일이나 애플리케이션 경로
- __params__: 애플리케이션에 전달될 매개변수
- __query__: 질의 문자열 또는 매개변수. 앰퍼샌드(&)로 구분된 이름=값 쌍 형식으로 표현
- __fragment__: 문서 내의 앵커 등 조각을 지정



#### 2.2.2 urllib.request 모듈

> urlopen(url, data = None, [timeout])



__urlopen() 함수__

```python
from urllib.request import urlopen
```



- GET 방식

```python
from urllib.request import urlopen

f = urlopen("http://www.example.com")
print(f.read(500).decode('utf-8'))
```



- POST 방식

```python
# 서버를 올리고 정보를 요청
winter@Winterui-MacBookPro ch2-test-server % python manage.py runserver

Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 4 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth.
Run 'python manage.py migrate' to apply them.
January 27, 2021 - 15:29:12
Django version 3.1.5, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
HomeView.post()...
python
django
홍길동
hong@gmail.com
http://google.co.kr
[27/Jan/2021 15:29:19] "POST / HTTP/1.1" 200 1758
```

```python
from urllib.request import urlopen

data = "language=python&framework=django"
f = urlopen("http://127.0.0.1:8000", bytes(data, encoding='utf-8'))

print(f.read(500).decode('utf-8'))
```



- Request 클래스로 요청 헤더 지정
  - 헤더값을 사용자가 모두 지정할 필요는 없으므로, 브라우저가 자동으로 지정하고 꼭 필요한 것만 지정
  - 헤더값이 상단에 표시됨

```python
from urllib.request import urlopen, Request
from urllib.parse import urlencode

url = 'http://127.0.0.1:8000'

data = {
    'name': '김석훈',
    'email': 'shkim@naver.com',
    'url': 'http://www.naver.com',
}
encData = urlencode(data)
postData = bytes(encData, encoding='utf-8')

req = Request(url, data=postData)
req.add_header('Content-Type', 'application/x-www-form-urlencoded')

f = urlopen(req)

print(f.info())
print(f.read(500).decode('utf-8'))
```

```
Date: Wed, 27 Jan 2021 06:36:54 GMT
Server: WSGIServer/0.2 CPython/3.9.0
Content-Type: text/html; charset=utf-8
X-Frame-Options: DENY
Content-Length: 1758
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin


<!DOCTYPE html>
<html lang="ko">




<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>ch2-test-server</title>

    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css">

    <!-- my css -->
    <link rel="shortcut
```



- HTTPBasicAuthHandler 클래스로 인증 요청

```python
from urllib.request import HTTPBasicAuthHandler, build_opener


auth_handler = HTTPBasicAuthHandler()
auth_handler.add_password(realm='ksh', user='shkim', passwd='shkimadmin', uri='http://127.0.0.1:8000/auth/')  # OK
# NOK. auth_handler.add_password(realm='ksh', user='shkim', passwd='shkimadmin', uri='http://127.0.0.1:8000/')
opener = build_opener(auth_handler) # 서버 인증 자격 빌드 (인증 Key값)
resp = opener.open('http://127.0.0.1:8000/auth/') # 서버 인증 요청
print(resp.read().decode('utf-8'))
```



- HTTPCookieProcessor 클래스로 쿠키 데이터를 포함하여 요청

```python
from urllib.request import Request, HTTPCookieProcessor, build_opener


url = 'http://127.0.0.1:8000/cookie/'

# first request (GET) with cookie handler

# 쿠키 핸들러 생성, 쿠키 데이터 저장은 디폴트로 CookieJar 객체를 사용함
cookie_handler = HTTPCookieProcessor()
opener = build_opener(cookie_handler)

req = Request(url)
res = opener.open(req)

print(res.info())
print(res.read().decode('utf-8'))

# second request (POST)
print("-------------------------------------------------------")

data = "language=python&framework=django"
encData = bytes(data, encoding='utf-8')

req = Request(url, encData)
res = opener.open(req)

print(res.info())
print(res.read().decode('utf-8'))
```



- ProxyHandler 및 ProxyBasicaAuthHandler 클래스로 프록시 처리
  - proxy: "방화벽"이라고 생각하면 된다

```python
import urllib.request


url = 'http://www.example.com'
proxyServer = 'http://www.proxy.com:3128/'

# 프록시 서버를 통해 웹서버로 요청을 보냅니다.
proxy_handler = urllib.request.ProxyHandler({'http': proxyServer})

# 프록시 서버 설정을 무시하고 웹서버로 요청을 보냅니다.
# proxy_handler = urllib.request.ProxyHandler({})

# 프록시 서버에 대한 인증을 처리합니다.
proxy_auth_handler = urllib.request.ProxyBasicAuthHandler()
proxy_auth_handler.add_password('realm', 'host', 'username', 'password')

# 2개의 핸들러를 오프너에 등록합니다.
opener = urllib.request.build_opener(proxy_handler, proxy_auth_handler)

# 디폴트 오프너로 지정하면, urlopen() 함수로 요청을 보낼 수 있습니다.
urllib.request.install_opener(opener)

# opener.open() 대신에 urlopen()을 사용했습니다.
f = urllib.request.urlopen(url)

print("geturl():", f.geturl())
print(f.read(300).decode('utf-8'))
```



#### 2.2.3 urllib.request 모듈 예제

```python
from urllib.request import urlopen
from html.parser import HTMLParser


class ImageParser(HTMLParser):
    def handle_starttag(self, tag, attrs):
        if tag != 'img':
            return
        if not hasattr(self, 'result'):
            self.result = []
        for name, value in attrs:
            if name == 'src':
                self.result.append(value)


def parse_image(data):
    parser = ImageParser()
    parser.feed(data)
    dataSet = set(x for x in parser.result)
    return dataSet


def main():
    url = "http://www.google.co.kr"

    with urlopen(url) as f:
        charset = f.info().get_param('charset')
        data = f.read().decode(charset)

    dataSet = parse_image(data)
    print("\n>>>>>>>>> Fetch Images from", url)
    print('\n'.join(sorted(dataSet)))


if __name__ == '__main__':
    main()
```



#### 2.2.4 http.client 모듈

1. 연결객체 생성: conn = http.client.HTTPConnection("www.python.org")
2. 요청을 보냄: conn.request("GET", "/index.html")
3. 응답객체 생성: response = conn.getresponse()
4. 응답 데이터를 읽음: data = response.read()
5. 연결을 닫음: conn.close()



- GET 방식 요청

```python
from http.client import HTTPConnection

host = 'www.example.com'
conn = HTTPConnection(host)

conn.request('GET', '/')

r1 = conn.getresponse()
print(r1.status, r1.reason)

data1 = r1.read()
# 일부만 읽는 경우
# data1 = r1.read(100)

# 두번째 요청에 대한 테스트
conn.request('GET', '/')

r2 = conn.getresponse()
print(r2.status, r2.reason)

data2 = r2.read()
print(data2.decode())

conn.close()
```



- HEAD 방식 요청

```python
from http.client import HTTPConnection

conn = HTTPConnection('www.example.com')
conn.request('HEAD', '/')

resp = conn.getresponse()
print(resp.status, resp.reason)

data = resp.read()
print(len(data))
print(data == b'')
```



- POST방식 요청

```python
from http.client import HTTPConnection
from urllib.parse import urlencode

host = '127.0.0.1:8000'
params = urlencode({
    'language': 'python',
    'name': '김석훈',
    'email': 'shkim@naver.com',
})
headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'text/plain',
}

conn = HTTPConnection(host)
conn.request('POST', '', params, headers)
resp = conn.getresponse()
print(resp.status, resp.reason)

data = resp.read()
print(data.decode('utf-8'))

conn.close()
```



- PUT 방식 요청

```python
from http.client import HTTPConnection
from urllib.parse import urlencode


host = '127.0.0.1:8000'
params = urlencode({
    'language': 'python',
    'name': '김석훈',
    'email': 'shkim@naver.com',
})
headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'text/plain',
}

conn = HTTPConnection(host)
conn.request('PUT', '', params, headers)
resp = conn.getresponse()
print(resp.status, resp.reason)

data = resp.read(300)
print(data.decode('utf-8'))

conn.close()
```



__http.client 모듈 예제__

```python
import os
from http.client import HTTPConnection
from urllib.parse import urljoin, urlunparse
from urllib.request import urlretrieve
from html.parser import HTMLParser


class ImageParser(HTMLParser):
    def handle_starttag(self, tag, attrs):
        if tag != 'img':
            return
        if not hasattr(self, 'result'):
            self.result = []
        for name, value in attrs:
            if name == 'src':
                self.result.append(value)


def download_image(url, data):

    if not os.path.exists('DOWNLOAD'):
        os.makedirs('DOWNLOAD')

    parser = ImageParser()
    parser.feed(data)
    dataSet = set(x for x in parser.result)

    for x in sorted(dataSet) :
        imageUrl = urljoin(url, x)
        basename = os.path.basename(imageUrl)
        targetFile = os.path.join('DOWNLOAD', basename)

        print("Downloading...", imageUrl)
        urlretrieve(imageUrl, targetFile)


def main():
    host = "www.google.co.kr"

    conn = HTTPConnection(host)
    conn.request("GET", '')
    resp = conn.getresponse()

    charset = resp.msg.get_param('charset')
    data = resp.read().decode(charset)
    conn.close()

    print("\n>>>>>>>>> Download Images from", host)
    url = urlunparse(('http', host, '', '', '', ''))
    download_image(url, data)


if __name__ == '__main__':
    main()
```



### 2.3 웹 서버 라이브러리

#### 2.3.1 간단한 웹서버

```

```





#### 2.3.2 HTTPServer 및 BaseHTTPRequestHandler 클래스



#### 2.3.3 SimpleHTTPRequestHandler



#### 2.3.4 CGIHTTPRequestHandler 클래스





### 2.4 CGI/WSGI 라이브러리

- CGI: 서버 부하가 높아짐
- WSGI: CGI의 단점을 해결하고 파이썬으로 애플리케이션을 좀 더 쉽게 작성할 수 있도록 웹 서버와 애플리케이션 간 연동 규격을 정의한 것



#### 2.4.3 WSGI 서버의 애플리케이션 처리 과정



#### 2.4.4 wsgiref.simple_server 모듈

```python
from wsgiref.simple_server import make_server


def my_app(environ, start_response):

    status = '200 OK'
    headers = [('Content-Type', 'text/plain')]
    start_response(status, headers)

    response = [b"This is a sample WSGI Application."]

    return response


if __name__ == '__main__':
    print("Started WSGI Server on port 8787...")
    server = make_server('', 8787, my_app)
    server.serve_forever()
```





