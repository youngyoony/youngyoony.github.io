---
title: "Self-Study Basic Python Data Analysis: *Chapter 01*"
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



## 01-1 데이터 분석이란<br>
**NumPy**<br>
Numerical Python의 줄임말로, 고성능 과학 계산과 다차원 배열(array)를 위한 파이썬 패키지임. 대부분의 파이썬 데이터 분석 패키지는 넘파이 배열을 사용함.<br><br>

**Pandas**<br>
파이썬 데이터 분석을 위한 전문 패키지. 데이터프레임(DataFrame) 사용. 넘파이가 계산에 초점을 맞추었다면, 판다스는 편리한 데이터 처리와 분석 작업 용도. 그래프 출력 기능 탑재.<br><br>

**matplotlib**<br>
파이썬 데이터 시각화를 위한 기본 패키지. 다른 파이썬 패키지와의 호환성이 높음. 이외에 seaborn, bokeh와 같은 시각화 패키지를 많이 사용<br><br>

**SciPy**<br>
넘파이를 기반으로 구축된 수학과 과학 계산 전문 패키지. 미분, 적분, 확률, 선형대수, 최적화를 알고리즘으로 구현.<br><br>

**Scikit-learn**<br>
파이썬의 머신러닝 패키지로, 넘파이와 사이파이에 의존함.<br><br>


## 01-2 도서관 예시 데이터 읽기<br>
**csv 파일 열기**<br>
```python
import chardet
with open('namsan.csv', mode='rb') as f:
    d = f.readline()
print(chardet.detect(d)) # 파일 인코딩 형식 확인

with open('namsan.csv', encoding='EUC-KR') as f:
    print(f.readline() # csv 파일 처음 몇 줄을 출력
```
<br>br

**Pandas에서 csv 파일 열기**<br>
```python
import pandas as pd
df = pd.read_csv('namsan.csv', encoding='EUC-KR', low_memory=False) # low_memory를 False로 지정 시, csv 파일을 한 번에 모두 읽어서 많은 메모리를 사용함.
df = pd.read_csv('namsan.csv', encoding='euc_kr', dtype={'ISBN': str, '세트 ISBN': str, '주제분류번호': str}) # 문제가 생긴 데이터 타입을 문자열로 지정하여 읽는 코드
df.head()
```
<br>
{% raw %}<img src="https://youngyoony.github.io/assets/images/da0102_dfhead.png" alt="">{% endraw %}<br>
* 첫 번째 열은 데이터프레임의 Index임. 판다스는 행마다 0부터 시작하는 인덱스 번호를 자동으로 붙여 줌.<br>
* csv의 첫 번째 행은 열 이름으로 인식. 첫 행을 열 이름으로 인식하지 않게 하려면 header 매개변수를 None으로 지정 & names 매개변수에 열 이름 리스트를 따로 전달. (names는 중복된 이름이 있어선 안 됨.)<br><br>

```python
df.to_csv('namsan_202405.csv') # 저장하기

with open('namsan_202405.csv') as f:
    for i in range(3):
        print(f.readline(), end='') # 3줄 읽어오기 end=''는 줄바꿈 문자를 출력하지 않음
```<br>
```python
ns_df = pd.read_csv('namsan_202405.csv', low_memory=False)
ns_df.head() # 이 경우 index까지 출력되게 됨
ns_df = pd.read_csv('namsan_202405.csv', index_col=0, low_memory=False)
ns_df.head() # 이 경우 index 제외됨
################
df.to_csv('namsan_202405.csv', index=False) # 아니면 저장할 때부터 이렇게 저장하는 방법이 있음
```

**Summary** 1\. 파이썬에서 가장 많이 쓰이는 데이터분석 패키지를 확인했다.<br>
2\. Pandas로 데이터를 불러왔다.
{: .notice--success}

