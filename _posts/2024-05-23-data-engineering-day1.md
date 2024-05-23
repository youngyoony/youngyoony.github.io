---
title: "Data Engineering Study: *Day 1*"
header:
  overlay_color: "#333"
categories:
  - Data Engieneering
tags:
  - data engineering
toc: false
toc_sticky: false
---


데이터 엔지니어링 포트폴리오 진행 과정을 정리하는 페이지입니다.<br>
This page documents the progress of my data engineering portfolio.<br><br><br>

## 목표
- 데이터를 주기적으로 수집하고 pyspark를 사용하여 정제하기
- 정제한 데이터를 저장하고 kibana로 시각화를 생성하기
- 자동으로 파이프라인을 실행하기 위해 Airflow job을 생성하기

## Tool: Spark, Airflow, Kibana<br><br>

**Spark** 
Scala로 쓰여졌지만 소통과 범용성을 위해 Python으로 진행 예정<br><br>

## Distributed System
Local File System / DFS 측면에서 Hadoop을 주로 쓰는데, 너무 복잡해서 Spark를 사용하게 됨. Spark는 분산 데이터처리 프레임워크로서, 주로 데이터 처리에 사용함. (다양한 데이터 포맷, 처리 방법, 데이터 저장소 사용 가능.)
> Hadoop은 디스크에서, Spark는 메모리에서.

Cluster Manager (쿠버네티스 등) 는 이미 잘 만들어진 솔루션들이 많음. 그래서 Spark에는 붙이지 않음. 각자 사용하는 Cluster Manager를 붙여 쓸 수 있게 함. yarn, mesos, k8s(쿠버네티스) + local

데이터가 들어오면 데이터를 적절히 잘라서 클러스터에 보내줘야 함. 그 역할을 distributed file system이 맡음 (기 존재하는 솔루션 활용 hdfs-Hadoop의-) - 그래서 Spark를 설치할 때 Hadoop도 설치하게 되는 것.

