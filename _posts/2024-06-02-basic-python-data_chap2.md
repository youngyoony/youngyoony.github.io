---
title: "Self-Study Basic Python Data Analysis: *Chapter 02*"
header:
  overlay_color: "#333"
categories:
  - Data Analysis
tags:
  - Data Analysis
  - Python
toc: true
toc_sticky: true
---


혼자 공부하는 데이터분석 with 파이썬 (박해선 저, 한빛미디어) 서적을 혼자 공부하며 정리하는 페이지입니다.<br>
This page is for summarizing my self-study of the book “Data Analysis with Python: Self-Study” by Haeseon Park, published by Hanbit Media. A brief English version is provided below.<br><br><br>



## 02-1 데이터 불러오기<br>
**API**<br>
* 두 프로그램이 서로 대화하기 위한 방법을 정의한 것.<br>
* 웹 사이트는 웹 페이지를 전송하기 위해 웹 서버 소프트 웨어를 사용한다. (NGINX, Apache) 통신 규약<br>
* HTTP는 인터넷에서 웹 페이지를 전송하는 기본 통신 방법 - Web Server to Web Browser(웹 데이터 요청(HTML)), Web Browser to Web Server(웹 데이터 요청(HTTP)). 이러한 HTTP 프로토콜을 사용해 API를 만드는 것이 웹 기반 API, 웹 기반 API를 만드는 것은 Software Engineer이고, 웹 기반 API를 사용하는 방법을 아는 게 데이터 분석가.<br>
* HTML은 웹 브라우저가 화면에 표시할 수 있는 문서의 한 종류이자 웹 페이지를 위한 표준 언어임.<br>
* HTTP로 데이터를 요청할 떄 CSV, JSON, XML 등을 선호하는 이유는 훨씬 간단하기 때문임. 특히 웹 기반 API에는 CSV보다는 JSON과 XML을 많이 사용함. CSV는 각 행마다 항목의 개수가 정확히 맞지 않으면 읽을 수 없고, 행과 열로만 구성되어 복잡한 데이터 구조를 표현하기 어렵다.<BR>
**JSON**<br>
* JavaScript Object Notation의 약자임. 원래는 자바스크립트 언어를 위해 만들어졌지만 현재는 범용적인 포맷으로 사용.<br>
* 파이썬의 Dictionary와 List를 중첩해 놓은 형태. (e.g. {"name": "혼자 공부하는 데이터 분석"}<br>
```python
d = {"name": "혼자 공부하는 데이터 분석"} # JSON 형식은 키과 값에 큰따옴표 사용.
print(d['name'])
```
<br>
* 파이썬 json 패키지를 사용해 딕셔너리 d를 JSON에 맞는 문자열로 바꾸기. - 프로그램상의 객체를 저장하거나 읽을 수 있는 형태로 변환하는 것을 직렬화(Serialization)이라고 함<br>
```python
d_str = json.dumps(d, ensure_ascii=False) # ensure_ascii 매개변수를 False로 지정한 이유는 딕셔너리 d에 한글이 포함되어 있기 때문임. json.dumps()는 ASCII 문자 외 다른 문자를 16진수로 출력함.
print(d_str)
print(type(d_str))
```
* JSON 문자열을 파이썬 객체로 변환. - 직렬화된 정보를 다시 프로그램에서 실행 가능한 객체로 변환하는 것을  직렬화(Deserialization)이라고 함<br>
```python
d_str = json.dumps(d, ensure_ascii=False) # ensure_ascii 매개변수를 False로 지정한 이유는 딕셔너리 d에 한글이 포함되어 있기 때문임. json.dumps()는 ASCII 문자 외 다른 문자를 16진수로 출력함.
print(d_str)
print(type(d_str))
```
