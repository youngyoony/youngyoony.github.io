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



## 01-1 Artificial Intelligence, Machine Learning, Deep Learning<br>
**Artificial Intelligence**<br>
Technology to create computer systems that can learn and reason like humans.<br><br>

**Machine Learning**<br>
A field of study that focuses on algorithms that automatically learn rules from data without needing to be explicitly programmed. It is a subfield of artificial intelligence that handles software to implement intelligence.<br>
* Scikit-learn: A machine learning library using the Python API. It can be conveniently used with classes and functions provided by the Scikit-learn library. However, new machine learning algorithms are not quickly updated and are added after being sufficiently verified. Chapters 1 to 6 of this book cover machine learning algorithms included in Scikit-learn.<br><br>

**Deep Learning**<br>
Among machine learning algorithms, methods based on artificial neural networks are called deep learning.<br>
* TensorFlow: Google’s open-source deep learning library. Chapters 7 to 9 of this book cover algorithms using deep learning with TensorFlow.<br>
* PyTorch: Facebook’s open-source deep learning library.<br><br>


## 01-2 Colab and Jupyter Notebook<br>
**Google Colab**<br>
A cloud-based Jupyter Notebook development environment. In other words, a service that allows you to test and save Python programs for free in a web browser. [link](https://colab.research.google.com "Colab").<br>
Here, text cells (the minimum unit that can be executed in Colab, using Markdown and HTML), code cells, and output sections are distinguished.<br>

**Jupyter**<br>
Refers to an interactive programming environment. The representative product of the Jupyter project is the Notebook.<br><br>


## 01-3 Market and Machine Learning Practice<br>
**Fish Classification Problem**<br>

<b>1-1. Bream Size Sample</b>
```python
bream_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0]
bream_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0]
```

<b>1-2. Plotting Bream Scatter Plot with matplotlib</b>
```python
import matplotlib.pyplot as plt
plt.scatter(bream_length, bream_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_scatterplot.png" alt="">{% endraw %}<br><br>

<b>2-1. Smelt Size Sample</b>
```python
smelt_length = [9.8, 10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
smelt_weight = [6.7, 7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
``

<b>2-2. Plotting Smelt Scatter Plot with matplotlib</b>
```python
plt.scatter(bream_length, bream_weight)
plt.scatter(smelt_length, smelt_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()<br><br>
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_scatterplot2.png" alt="">{% endraw %}

<b>3\. Checking k-Nearest Neighbors</b>
```python
length = bream_length + smelt_length
weight = bream_weight + smelt_weight
fish_data = [[l, w] for l, w in zip(length, weight)] # List consisting of [l,w] as one element
print(fish_data)
```
<span style="font-size:80%">✔︎ The zip() function extracts elements one by one from the listed lists.</span>  <br><br>


<b>4\. Distinguish Bream as 1 and Smelt as 0 (Eventually, there should be 35 Breams and 14 Smelts)</b>
```python
fish_target = [1] * 35 + [0] * 14
print(fish_target)
```
<span style="font-size:80%">✔︎ In machine learning, when distinguishing two, the target is set as 1, and others as 0.</span><br><br>


<b>5\. Using Sklearn and KNeighborsClassifier</b>
```python
from sklearn.neighbors import KNeighborsClassifier
```
<span style="font-size:80%">✔︎ This code is identical to the following code.</span>  
```python
import sklearn
model = sklearn.neighbors.KNeighborsClassifier()
```
```python
kn = KNeighborsClassifier() #Creating an object of KNeighborsClassifier 
```
<span style="font-size:80%">✔︎ This object is trained to find criteria for Bream by passing fish_data and fish_target = Training</span>  
```python
kn.fit(fish_data, fish_target)
```
<span style="font-size:80%">✔︎ The fit() method trains the algorithm with the given data.</span>  
```python
kn.score(fish_data, fish_target)
```
<span style="font-size:80%">✔︎ The score() method evaluates how well the model kn is trained. An accuracy of 1 means all data were correctly matched, 0 means all were incorrect. Here, ‘model’ refers to a program implementing the machine learning algorithm.</span><br><br>

<b>6\. Explanation of k-Nearest Neighbors Algorithm</b><br>
When finding an answer for some data, look at other nearby data and use the majority as the answer. To predict new data, just look at which data is closest in straight-line distance.
A disadvantage is that it is difficult to use when there is a large amount of data, and it requires a lot of memory.

```python
kn.predict([[30,600]])
```
The predict() method predicts the answer for new data. The predicted value of this point is 1. Since Bream is 1, the prediction is as expected.

```python
print(kn._fit_X)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_sklearn.png" alt="width=50px;height:auto;">{% endraw %}
```python
print(kn._fit_y)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_sklearn2.png" alt="">{% endraw %}
In other words, the k-Nearest Neighbors algorithm does not particularly train. It stores all the data in the fit() method and then references the closest data to determine whether it is a Bream or Smelt when new data appears.
The default value of the KNeighborsClassifier class is 5, and this criterion can be changed with the n_neighbors parameter.

```python
kn49 = KNeighborsClassifier(n_neighbors=49) #참고 데이터를 49개로 한 kn49 모델
kn49.fit(fish_data, fish_target)
kn49.score(fish_data, fish_target)
```
Since Breams take the majority of 35 out of 49 data in fish_data, it will always predict Bream for any data. The result of the above code is approximately 0.71428…, which is the same as the value of 35/49.<br>
```python
for n in range(5, 50):
    kn.n_neighbors = n
    score = kn.score(fish_data, fish_target)
    if score < 1:
        print(n, score)
        break
```
This changes n_neighbors from 5 to 49 to find the value where the score starts to drop below 1.
<br><br><br>

**Summary** 1\. Measure the length and weight of 35 Breams and 14 Smelts and create a Python list. Also, prepare the data by combining the Bream & Smelt data into a list of lists.<br>
2\. Used the k-Nearest Neighbors algorithm of Scikit-learn to predict data. This model predicts data by looking at the five closest data based on the majority rule.<br>
3\. Used the fit(), score(), and predict() methods of the KNeighborsClassifier class.
{: .notice--success}

<br><br><br><br><br>

## 01-1 인공지능과 머신러닝, 딥러닝<br>
**Artificial Intelligence**<br>
사람처럼 학습하고 추론할 수 있는 지능을 가진 컴퓨터 시스템을 만드는 기술<br><br>

**Machine Learning**<br>
규칙을 일일이 프로그래밍하지 않아도 자동으로 데이터에서 규칙을 학습하는 알고리즘을 연구하는 분야. 인공지능의 하위 분야 중 지능을 구현하기 위한 소프트웨어를 담당함.<br>
* Scikit-learn: 파이썬 API를 사용한 머신러닝 라이브러리. 사이킷런 라이브러리에서 제공하는 클래스와 함수로 편하게 사용, 그러나 신규 머신러닝 알고리즘이 빠르게 업데이트 되지는 않고, 충분히 검증된 뒤 추가됨. 이 책의 1장부터 6장까지 사이킷런에 포함된 머신러닝 알고리즘들을 다룸.<br><br>

**Deep Learning**<br>
머신러닝 알고리즘 중에서 인공 신경망(artificial neural network)을 기반으로 한 방법들을 딥러닝이라고 부름. <br>
* TensorFlow: 구글의 오픈소스 딥러닝 라이브러리. 이 책의 7장부터 9장까지 TensorFlow를 사용한 딥러닝을 사용한 알고리즘을 다룸.<br>
* PyTorch: 페이스북의 오픈소스 딥러닝 라이브러리.<br><br>


## 01-2 코랩과 주피터 노트북<br>
**Google Colab**<br>
클라우드 기반의 주피터 노브툭 개발 환경. 즉, 웹 브라우저에서 무료로 파이썬 프로그램을 테스트하고 저장할 수 있는 서비스. [link](https://colab.research.google.com "Colab").<br>
여기서 텍스트 셀(cell - 코랩에서 실행할 수 있는 최소 단위 / 마크다운, HTML 사용 가능)과 코드 셀, 출력 란이 구분됨.<br>

**Jupyter**<br>
대화식 프로그래밍 환경을 의미함. 주피터 프로젝트의 대표 제품이 Notebook임.<br><br>


## 01-3 마켓과 머신러닝 실습<br>
**생선 분류 문제**<br>

<b>1-1. 도미 사이즈 샘플</b>
```python
bream_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0]
bream_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0]
```

<b>1-2. matplotlib으로 도미 산점도 그리기</b>
```python
import matplotlib.pyplot as plt
plt.scatter(bream_length, bream_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_scatterplot.png" alt="">{% endraw %}<br><br>

<b>2-1. 빙어 사이즈 샘플</b>
```python
smelt_length = [9.8, 10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
smelt_weight = [6.7, 7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
``

<b>2-2. matplotlib으로 빙어 산점도 그리기</b>
```python
plt.scatter(bream_length, bream_weight)
plt.scatter(smelt_length, smelt_weight)
plt.xlabel('length')
plt.ylabel('weight')
plt.show()<br><br>
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_scatterplot2.png" alt="">{% endraw %}

<b>3\. k-최근접 이웃 확인</b>
```python
length = bream_length + smelt_length
weight = bream_weight + smelt_weight
fish_data = [[l, w] for l, w in zip(length, weight)] # [l,w]가 하나의 원소로 구성된 리스트
print(fish_data)
```
<span style="font-size:80%">✔︎ zip() 함수는 나열된 리스트에서 원소를 하나씩 꺼내주는 일을 한다.</span>  <br><br>


<b>4\. 도미는 1, 빙어는 0으로 구분 (최종적으로 도미 35마리, 빙어 14마리가 나와야 함)</b>
```python
fish_target = [1] * 35 + [0] * 14
print(fish_target)
```
<span style="font-size:80%">✔︎ 머신러닝에서 2개를 구분하는 경우 찾으려는 대상을 1로, 그 외에는 0으로 놓는다.</span><br><br>


<b>5\. Sklearn 및 KNeighborsClassifier 활용하기</b>
```python
from sklearn.neighbors import KNeighborsClassifier
```
<span style="font-size:80%">✔︎ 이 코드는 하단 코드와 동일한 코드다.</span>  
```python
import sklearn
model = sklearn.neighbors.KNeighborsClassifier()
```
```python
kn = KNeighborsClassifier() #KNeighborsClassifier 클래스의 객체 만들기
```
<span style="font-size:80%">✔︎ 이 객체에 fish_data와 fish_target을 전달하여 도미를 찾기 위한 기준을 학습시키기 = 훈련(training)</span>  
```python
kn.fit(fish_data, fish_target)
```
<span style="font-size:80%">✔︎ fit() 메서드는 주어진 데이터로 알고리즘을 훈련시킨다.</span>  
```python
kn.score(fish_data, fish_target)
```
<span style="font-size:80%">✔︎ score() 메서드는 모델 kn이 얼마나 잘 훈련되었는지를 평가하는 메서드다. = 정확도(accuracy) 1은 모든 데이터를 정확히 맞혔다는 것을 의미, 0은 전부 틀렸다는 걸 의미한다. 여기서 '모델'은 머신러닝 알고리즘을 구현한 프로그램을 의미한다.</span><br><br>

<b>6\. k-최근접 이웃 알고리즘 설명</b><br>
어떤 데이터에 대한 답을 구할 때 주위의 다른 데이터를 보고 다수를 차지하는 것을 정답으로 사용한다. 새로운 데이터에 대해 예측할 떄는 가장 가까운 직선거리에 어떤 데이터가 있는지를 살피기만 하면 된다.
단점으로는, 이런 특징 때문에 데이터가 아주 많은 경우에는 사용하기 어려우며, 메모리가 많이 필요하다는 단점이 있다.

```python
kn.predict([[30,600]])
```
predict() 메서드는 새로운 데이터의 정답을 예측한다. 이 포인트의 예측값은 1이다. 도미는 1이므로 예상과 같다.

```python
print(kn._fit_X)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_sklearn.png" alt="width=50px;height:auto;">{% endraw %}
```python
print(kn._fit_y)
```
{% raw %}<img src="https://youngyoony.github.io/assets/images/ml0103_sklearn2.png" alt="">{% endraw %}
즉, k-최근접 이웃 알고리즘은 특별히 훈련되는 게 없다. fit() 메서드에 데이터를 모두 저장하고 있다가 새로운 데이터가 등장하면 가장 가까운 데이터를 참고하여 도미인지 빙어인지를 구분한다.
KNeighborsClassifier 클래스의 기본값은 5이며, 이 기준은 n_neighbors 매개변수로 바꿀 수 있다.

```python
kn49 = KNeighborsClassifier(n_neighbors=49) #참고 데이터를 49개로 한 kn49 모델
kn49.fit(fish_data, fish_target)
kn49.score(fish_data, fish_target)
```
fish_data의 데이터 49개 중에 도미가 35개로 다수를 차지하기 때문에, 어떤 데이터를 넣어도 무조건 도미로 예측할 것이다. 위 코드의 결과는 대략 0.71428...이 나오는데, 이는 35/49의 값과 동일한 값이다.<br>
```python
for n in range(5, 50):
    kn.n_neighbors = n
    score = kn.score(fish_data, fish_target)
    if score < 1:
        print(n, score)
        break
```
이는 n_neighbors를 5부터 49까지 변경해가며, score가 1.0 아래로 내려가기 시작하는 수치를 찾은 것이다.
<br><br><br>

**Summary** 1\. 도미 35마리와 빙어 14마리의 길이와 무게를 측정해서 파이썬 리스트로 만든다. 또한 이 도미 & 빙어 데이터를 합쳐 리스트의 리스트로 데이터를 준비했다.<br>
2\. 사이킷런의 k-최근접 이웃 알고리즘을 사용해서 데이터를 예측했다. 이는 주변에서 가장 가까운 5개의 데이터를 보고 다수결의 원칙에 따라 데이터를 예측하는 모델이다.<br>
3\. KNeighborsClassifier 클래스의 fit(), score(), predict() 메서드를 사용했다.
{: .notice--success}

