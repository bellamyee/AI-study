# 그래프
## 그래프 관련 인공지능 문제
 - 정점 분류 문제(ex. 트위터에서의 retweet 관계를 분석하여, 각 사용자의 정치적 성향을 알 수 있을까? 단백질 상호작용을 분석해 단백질의 역할을 알아낼 수 있을까? 
 - 연결 예측 문제. 주어진 그래프가 어떻게 성장할지 예측(ex. 페이스북 소셜 네트워크의 진화 예측, 각 사용자가 어떤 물건을 구매할까, 만족할까 등 추천 문제) 
 - 군집 분석(community detection) 문제. 연결 관계로부터 사회적 무리(social circle)을 찾아낼 수 있을까?(clustering) 
 - 랭킹 및 정보 검색 문제. 웹 이라는 거대한 그래프로부터 어떻게 중요한 웹페이지를 찾아낼 수 있을까?
 - 정보 전파 및 바이럴 마케팅 문제. 정보는 네트워크를 통해 어떻게 전달될까? 어떻게 정보 전달을 최대화 할 수 있을까? 


## 그래프의 유형 및 분류
- 방향 및 가중치의 유무, 동종과 이종으로 구분 
![image](https://user-images.githubusercontent.com/43736669/108658246-c4b2aa00-750d-11eb-95ed-440870235ceb.png) 
![image](https://user-images.githubusercontent.com/43736669/108658910-f0ce2b00-750d-11eb-8724-929db2c8d619.png)
![image](https://user-images.githubusercontent.com/43736669/108659562-1bb87f00-750e-11eb-80fa-072fce299f2e.png)

- 그래프의 표현
 - 정점들의 집합을 V, 간선들의 집합을 E, 그래프를 G = (V,E)로 적음. 
 - 그래프와 연결된 다른 정점을 이웃이라고 표현. 이웃들의 집합을 N(v) 또는 Nv로 적음 
 ![image](https://user-images.githubusercontent.com/43736669/108661064-7d78e900-750e-11eb-8acf-05176b6dd0d5.png)
 - 방향성이 있는 그래프에서는 나가는 이웃과 들어오는 이웃을 구분하는데, Nout(V) Nin(V)로 표현
 ![image](https://user-images.githubusercontent.com/43736669/108661217-a13c2f00-750e-11eb-914c-1f5d01680a8d.png)
 - 파이썬에서는 networkX, snap.py 등의 라이브러리 사용


## 실제 그래프와 랜덤 그래프
 - 에르되스 레니 랜덤 그래프 G(n,p)
  - 임의의 두 정점 사이에 간선이 존재하는지 여부는 동일한 확률 분포에 의해 결정됨
  - n개의 정점을 가지며 두 정점 사이 간선이 존재할 확률은 p
  - 정점 간의 연결은 서로 독립적(영향을 끼치지 않음)
  
  - ex. G(3, 0.3) 에 의해 생성될 수 있는 그래프와 각각의 확률은?
  ![image](https://user-images.githubusercontent.com/43736669/108663515-13634280-7514-11eb-9a2f-8d929649eb9c.png)

## 경로
 - 정점 u와 v사이의 경로는 아래 조건을 만족하는 정점들의 순열(sequence)
 ![image](https://user-images.githubusercontent.com/43736669/108663594-47d6fe80-7514-11eb-9267-a4b486654313.png)
 ![image](https://user-images.githubusercontent.com/43736669/108663617-54f3ed80-7514-11eb-86f4-058202135e38.png)
 - 경로의 길이는 당 경로 상에 놓이는 간선의 수
 - 그래프의 지름(Diameter)은 정점 간 거리의 최댓값

## 작은 세상 효과(small-world effect) 
 - 임의의 두 사람을 골랐을 때, 평균적으로 6단계를 거쳐 연결되어 있음(편지 이용) 
 - MSN 그래프에선 평균 거리가 7(거대 연결 구조만 고려)
 - 체인, 사이클, 격자(Grid) 그래프에서는 존재하지 않음
 ![image](https://user-images.githubusercontent.com/43736669/108663893-ecf1d700-7514-11eb-8fbe-ff621987f8f4.png)

## 연결성(Degree)
 - 정점의 연결성(Degree)은 정점과 연결된 간선의 수
 - 나가는 연결성(dout), 들어오는 연결성(din) 으로도 표시
 - 실제 그래프의 연결성 분포는 두터운 꼬리(heavy tail)을 가짐 : 허브 정점이 존재
 ![image](https://user-images.githubusercontent.com/43736669/108663996-2cb8be80-7515-11eb-9cf9-f9e41a4bda71.png)
 - 랜덤 그래프의 연결성 분포는 높은 확률로 정규 분포와 유사 : 허브가 존재할 가능성은 0에 가까움
 - 정리 사진
 ![image](https://user-images.githubusercontent.com/43736669/108664055-4eb24100-7515-11eb-98b3-8afc81cdabfa.png)
 
## 연결 요소(Connected Component)
 - 1)연결 요소에 속하는 정점들은 경로로 연결될 수 있음
 - 2)1)의 조건을 만족하면서 정점을 추가할 수 없음 
 ![image](https://user-images.githubusercontent.com/43736669/108664123-71445a00-7515-11eb-85de-b65bfc9d084d.png)
 ![image](https://user-images.githubusercontent.com/43736669/108664158-80c3a300-7515-11eb-899a-82fe703ab95e.png)

