---
title: "Self-Study Machine Learning + Deep Learning: *Chapter 01*"
header:
  overlay_color: "#333"
categories:
  - Machine Learning
tags:
  - machine learning
  - deep learning
toc: true
toc_sticky: true
---


혼자 공부하는 머신러닝+딥러닝 (박해선 저, 한빛미디어) 서적을 혼자 공부하며 정리하는 페이지입니다.<br>
This page is for summarizing my self-study of the book “Self-Study Machine Learning + Deep Learning” by Haesun Park, published by Hanbit Media. A brief English version is provided below.<br><br><br>


## 01-1 인공지능과 머신러닝, 딥러닝<br>
**Artificial Intelligence**<br>
사람처럼 학습하고 추론할 수 있는 지능을 가진 컴퓨터 시스템을 만드는 기술<br><br>

**Machine Learning**<br>
규칙을 일일이 프로그래밍하지 않아도 자동으로 데이터에서 규칙을 학습하는 알고리즘을 연구하는 분야. 인공지능의 하위 분야 중 지능을 구현하기 위한 소프트웨어를 담당함.<br>
* Scikit-learn: 파이썬 API를 사용한 머신러닝 라이브러리. 사이킷런 라이브러리에서 제공하는 클래스와 함수로 편하게 사용, 그러나 신규 머신러닝 알고리즘이 빠르게 업데이트 되지는 않고, 충분히 검증된 뒤 추가됨. 이 책의 1장부터 6장까지 사이킷런에 포함된 머신러닝 알고리즘들을 다룸.<br><br>

**Deep Learning**<br>
머신러닝 알고리즘 중에서 인공 신경망(artificial neural network)을 기반으로 한 방법들을 딥러닝이라고 부름. <br>
* TensorFlow: 구글의 오픈소스 딥러닝 라이브러리. 이 책의 7장부터 9장까지 TensorFlow를 사용한 딥러닝을 사용한 알고리즘을 다룸.<br>
* PyTorch: 페이스북의 오픈소스 딥러닝 라이브러리.<br><br><br>


## 01-2 코랩과 주피터 노트북<br>
**Google Colab**<br>
클라우드 기반의 주피터 노브툭 개발 환경. 즉, 웹 브라우저에서 무료로 파이썬 프로그램을 테스트하고 저장할 수 있는 서비스. [link](https://colab.research.google.com "Colab").<br>
여기서 텍스트 셀(cell - 코랩에서 실행할 수 있는 최소 단위 / 마크다운, HTML 사용 가능)과 코드 셀, 출력 란이 구분됨.<br>

**Jupyter**<br>
대화식 프로그래밍 환경을 의미함. 주피터 프로젝트의 대표 제품이 Notebook임.<br><br><br>


## 01-3 마켓과 머신러닝<br>
**생선 분류 문제**<br>

1-1. 도미 사이즈 샘플
```python
bream_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0]
bream_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0]
```

1-2. matplotlib으로 도미 산점도 그리기
```python
import matplotlib.pyplot as plt
plt.scatter(bream_length, bream_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_scatterplot.png" alt="">{% endraw %}

2-1. 빙어 사이즈 샘플
```python
smelt_length = [9.8, 10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
smelt_weight = [6.7, 7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```

2-2. matplotlib으로 빙어 산점도 그리기
```python
plt.scatter(bream_length, bream_weight)
plt.scatter(smelt_length, smelt_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```

3-1. k-최근접 이웃 확인
```python
length = bream_length + smelt_length
weight = bream_weight + smelt_weight
fish_data = [[l, w] for l, w in zip(length, weight)] # [l,w]가 하나의 원소로 구성된 리스트
print(fish_data)
```

4-1. 도미는 1, 빙어는 0으로 구분 (최종적으로 )