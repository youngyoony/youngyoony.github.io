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



# 02-1 데이터 불러오기<br>
## API<br>
* 두 프로그램이 서로 대화하기 위한 방법을 정의한 것.<br>
* 웹 사이트는 웹 페이지를 전송하기 위해 웹 서버 소프트 웨어를 사용한다. (NGINX, Apache) 통신 규약<br>
* HTTP는 인터넷에서 웹 페이지를 전송하는 기본 통신 방법 - Web Server to Web Browser(웹 데이터 요청(HTML)), Web Browser to Web Server(웹 데이터 요청(HTTP)). 이러한 HTTP 프로토콜을 사용해 API를 만드는 것이 웹 기반 API, 웹 기반 API를 만드는 것은 Software Engineer이고, 웹 기반 API를 사용하는 방법을 아는 게 데이터 분석가.<br>
* HTML은 웹 브라우저가 화면에 표시할 수 있는 문서의 한 종류이자 웹 페이지를 위한 표준 언어임.<br>
* HTTP로 데이터를 요청할 떄 CSV, JSON, XML 등을 선호하는 이유는 훨씬 간단하기 때문임. 특히 웹 기반 API에는 CSV보다는 JSON과 XML을 많이 사용함. CSV는 각 행마다 항목의 개수가 정확히 맞지 않으면 읽을 수 없고, 행과 열로만 구성되어 복잡한 데이터 구조를 표현하기 어렵다.<br><br>

## JSON<br>
* JavaScript Object Notation의 약자임. 원래는 자바스크립트 언어를 위해 만들어졌지만 현재는 범용적인 포맷으로 사용.<br>
* 파이썬의 Dictionary와 List를 중첩해 놓은 형태. (e.g. {"name": "혼자 공부하는 데이터 분석"}<br>
```python
d = {"name": "혼자 공부하는 데이터 분석"} # JSON 형식은 키과 값에 큰따옴표 사용.
print(d['name'])
```
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
```python
d2 = json.loads(d_str)
print(d2['name'])
print(type(d2))
```
* 여러 개의 항목을 지닌 JSON 문자열을 json.loads() 함수에 직접 전달
```python
dd3 = json.loads('{"name": "Data Analysis with Python: Self-Study", "author": "박해선", "year": 2022}')
print(d3['name'])
print(d3['author'])
print(d3['year'])
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_json.png" alt="">{% endraw %}<br>
```python
d3 = json.loads('{"name": "Data Analysis with Python: Self-Study", "author": ["박해선", "홍길동"], "year": 2022}')
print(d3['author'][1])
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_json2.png" alt="">{% endraw %}<br>
```python
d4_str = """
[
    {"name": "Data Analysis with Python: Self-Study", "author": "박해선", "year": 2022},
    {"name": "Data Analysis with Python: ML+DL", "author": "박해선", "year": 2022}
]
"""
d4 = json.loads(d4_str)
print(d4[0]['name'])
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_json3.png" alt="">{% endraw %}<br>
* JSON 문자열을 데이터프레임으로 변환하기
```python
import pandas as pd
pd.read_json(d4_str)
pd.DataFrame(d4)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_json4.png" alt="">{% endraw %}<br><br>
## XML<br>
* XML: eXtensible Markup Language<br>
* XML은 엘리먼트(element)들이 계층 구조를 이루면서 정보를 표현. 태그는 <기호로 시작해서 >기호로 끝남.<br>
* XML 문자열을 파이썬 객체로 변환하기 (Deserialization)<br>
```python
import xml.etree.ElementTree as et
book = et.fromstring(x_str)
print(type(book))
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml.png" alt="">{% endraw %}<br>
* book 변수의 타입 확인.
```python
print(book.tag)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml2.png" alt="">{% endraw %}<br>
* book 객체의 tag 속성을 출력하면 엘리먼트 이름을 쉽게 확인할 수 있음.
```python
print(book.tag)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml3.png" alt="">{% endraw %}<br>
```python
book_childs = list(book)
print(book_childs)
```
* 리스트로 변환 시에는 list() 함수를 사용함.
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml4.png" alt="">{% endraw %}<br>
* 자식 엘리먼트가 잘 출력되었음
```python
name, author, year = book_childs
print(name.text)
print(author.text)
print(year.text)
```
* book_childs 리스트 각 항목을 name, author, year 변수에 할당하고 text 속성으로 element에 있는 텍스트를 출력.
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml5.png" alt="">{% endraw %}<br>
* 그러나 XML은 자식 엘리먼트 순서가 항상 일정하다는 것을 보장하지 않음.<br>
```python
name = book.findtext('name')
author = book.findtext('author')
year = book.findtext('year')
print(name)
print(author)
print(year)
```
* 따라서 findtext() 메서드를 사용하면 해당하는 자식 엘리먼트를 탐색하여 자동으로 텍스트를 반환함.<br>
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml6.png" alt="">{% endraw %}<br>
```python
x2_str = """
<books>
    <book>
        <name>Data Analysis with Python: Self-Study</name>
        <author>박해선</author>
        <year>2022</year>
    </book>
    <book>
        <name>Data Analysis with Python: ML+DL</name>
        <author>박해선</author>
        <year>2020</year>
    </book>
</books>
"""
books = et.fromstring(x2_str)
print(books.tag)
```
* fromstring() 함수를 사용해 부모 엘리먼트 확인
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml6.png" alt="">{% endraw %}<br>
```python
for book in books.findall('book'):
    name = book.findtext('name')
    author = book.findtext('author')
    year = book.findtext('year')
    print(name)
    print(author)
    print(year)
    print()
```
* <books>의 자식 엘리먼트를 모두 찾아 그 안에 담긴 텍스트를 잘 출력함.
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_xml7.png" alt="">{% endraw %}<br>
* JSON의 경우 API 전달 텍스트를 json.loads() 함수를 사용해 파이썬 객체로 바꾸어 내용 추출 <> XML은 xml.etree.ElementTree 모듈에 있는 fromstring() 함수를 사용하며 부모(루트) 엘리먼트를 얻고, findall() 메서드로 자식 엘리먼트에 담긴 텍스트를 추출할 수 있음.<br>
* pandas에서 xml을 읽어오는 방법<br>
```python
pd.read_xml(x2_str)
```
<br><br>
## API<br>
* XML: eXtensible Markup Language<br>
* XML은 엘리먼트(element)들이 계층 구조를 이루면서 정보를 표현. 태그는 <기호로 시작해서 >기호로 끝남.<br>