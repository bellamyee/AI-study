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
전체 그래프에서 시작하여 간선을 순차적으로 제거 
![image](https://user-images.githubusercontent.com/43736669/109108529-17db6580-7777-11eb-923f-1515cba0d653.png)  
다리 역할의 간선을 찾는 법 : 매개 중심성 높은 곳(정점 간의 최단 경로에 놓이는 횟수) 
![image](https://user-images.githubusercontent.com/43736669/109108604-36416100-7777-11eb-95ad-b2350f9f6a30.png) 
간선이 제가될 때마다, 매개 중심성을 다시 계산하여 갱신 
![image](https://user-images.githubusercontent.com/43736669/109108674-55d88980-7777-11eb-8ce0-74717eb92337.png) 
![image](https://user-images.githubusercontent.com/43736669/109108713-612bb500-7777-11eb-8b12-da85fa627fe6.png) 
![image](https://user-images.githubusercontent.com/43736669/109108736-6be64a00-7777-11eb-8581-d85066efc1a1.png)
간선의 제거 정도에 따라 다른 입도(Granularity)의 군집 구조가 나타남 
군집성이 최대가 되는 기준으로 간선을 제거. 현재의 연결 요소들을 군집으로 가정하되, 입력 그래프에서 군집성을 계산
![image](https://user-images.githubusercontent.com/43736669/109108842-9b955200-7777-11eb-9eb2-b20b6353d657.png)

## Girvan - Newman 알고리즘 요약
 1) 전체 그래프에서 시작
 2) 매개 중심성이 높은 순서로 간선을 제거하면서 군집성의 변화를 기록
 3) 군집성이 가장 커지는 상황을 복원
 4) 이 때, 서로 연결된 정점들, 즉 연결 요소를 하나의 군집으로 간주 
 즉, 전체 그래프에서 시작해서 점점 작은 단위를 검색하는 하향식(Top-Down) 방법 
 
## Louvain 알고리즘 
대표적인 상향식 군집 탐색 알고리즘 
개별 정점에서 시작하여 점점 큰 군집을 형성 
1) Louvain 알고리즘은 개별 정점으로 구성된 크기 1의 군집들로부터 시작  
![image](https://user-images.githubusercontent.com/43736669/109109515-ccc25200-7778-11eb-82dd-03bbc574010d.png) 
2) 각 정점 u를 기존 혹은 새로운 군집으로 이동. 이 때, 군집성이 최대화되도록 군집을 결정 
3) 더 이상 군집성이 증가하지 않을 때까지 2)를 반복 
![image](https://user-images.githubusercontent.com/43736669/109109607-f3808880-7778-11eb-8f3b-44d3513e50cc.png) 
4) 각 군집을 하나의 정점으로 하는 군집 레벨의 그래프를 얻은 뒤 3)을 수행합니다.
![image](https://user-images.githubusercontent.com/43736669/109109662-08f5b280-7779-11eb-8c04-4d2ab8f238e9.png) 
5) 한 개의 정점이 남을 때 까지 4를 반복 
 
# 중첩이 있는 군집 탐색 
## 중첩이 있는 군집 구조 
개인이 여러 군집에 속하게 되는 것.  
![image](https://user-images.githubusercontent.com/43736669/109109777-478b6d00-7779-11eb-87a5-117a681c3998.png)  
![image](https://user-images.githubusercontent.com/43736669/109109889-79043880-7779-11eb-821c-476d8f20698f.png)  

중첩 군집 모형이 주어지면, 주어진 그래프의 확률을 계산할 수 있음   
그래프의 확률은 다음 확률들의 곱  
1) 그래프의 각 간선의 두 정점이 직접 연결될 확률  
2) 그래프에서 직접 연결되지 않은 각 정점 쌍이 직접 연결되지 않을 확률  
![image](https://user-images.githubusercontent.com/43736669/109110059-bb2d7a00-7779-11eb-91e7-bb3f4aff9a18.png)  
중첩 군집 탐색은 주어진 그래프의 확률을 최대화하는 중첩 군집 모형을 찾는 과정. 즉 최우도 추정치를 찾는 과정(Maximum Likelihood Estimate)  
![image](https://user-images.githubusercontent.com/43736669/109110148-e617ce00-7779-11eb-8421-816cf83dd06b.png) 

## 완화된 중첩 군집 모형 
중첩 군집 탐색을 용이하게 하기 위해 완화된 중첩 군집 모형을 사용  
완화된 중첩 군집 모형에서는 각 정점이 각 군집에 속해 있는 정도를 실숫값으로 표현합니다  
![image](https://user-images.githubusercontent.com/43736669/109110342-4a3a9200-777a-11eb-8b96-2f1085c03bf4.png)  
최적화 관점에서는, 모형의 매개변수들이 실수값을 가지기 때문에  
익숙한 최적화 도구(경사하강법등)을 사용하여 모형을 탐색할 수 있다는 장점이 있음. 

