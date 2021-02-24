# 군집
## 군집의 정의
### 군집이란 다음 조건들을 만족하는 정점들의 집합
집합에 속하는 정점 사이에는 많은 간선이 존재
집합에 속하는 정점과 그렇지 않은 정점 사이에는 적은 수의 간선이 존재 
![image](https://user-images.githubusercontent.com/43736669/108930336-1df31880-7689-11eb-85c0-3b904eec52c7.png)
### 온라인 소셜 네트워크의 군집들은 사회적 무리(Social Circle)를 의미하는 경우가 많음
 ![image](https://user-images.githubusercontent.com/43736669/108930413-3a8f5080-7689-11eb-9066-946ec88cdeaa.png)
### 혹은 부정 행위, 조직 내의 분란 등이 표현되기도 함
 ![image](https://user-images.githubusercontent.com/43736669/108930460-5266d480-7689-11eb-9099-2bc554190f04.png)
### 키워드-광고주 그래프에서는 동일한 주제의 키워드들이 군집을 형성
 ![image](https://user-images.githubusercontent.com/43736669/108930514-690d2b80-7689-11eb-9372-f169b3f354e7.png)
## 실제 그래프에서의 군집들
뉴런간 연결 그래프에서는 군집들이 뇌의 기능적 구성 단위를 의미

![image](https://user-images.githubusercontent.com/43736669/108930587-85a96380-7689-11eb-9005-1403161a00fb.png)
## 군집 탐색 문제
 - 그래프를 여러 군집으로 잘 나누는 문제를 군집 탐색 문제(Community Detection)라고 함 
 - 보통은 각 정점이 한 개의 군집에 속하도록 군집을 나눔. Clustering과 상당히 유사
 - 성공적인 군집 탐색을 정의하자!
# 군집 구조의 통계적 유의성과 군집성
## 비교 대상 : 배치 모형
### 배치 모형
각 정점의 연결성을 보존한 상태에서 간선들을 재배치해서 얻은 그래프
 
 ![image](https://user-images.githubusercontent.com/43736669/108930746-d4ef9400-7689-11eb-8fbd-fd44e934baf3.png)
 
 배치 모형에서 임의의 두 정점 i와 j 사이에 간선이 존재할 확률은 두 정점의 연결성에 비례
 
## 군집성(Modularity)
그래프와 군집들의 집합 S가 주어졌다고 하자. 각 군집 𝑠 ∈ 𝑆가 군집의 성질을 잘 만족하는 지를 살펴보기 위해, 군집 내부의 간선의 수를 그래프와 배치 모형에서 비교

![image](https://user-images.githubusercontent.com/43736669/108931065-5fd08e80-768a-11eb-92e0-b385899bab1a.png)

# 군집 탐색 알고리즘
## Girvan - Newman 알고리즘
대표적인 하향식 군집 탐색 알고리즘
