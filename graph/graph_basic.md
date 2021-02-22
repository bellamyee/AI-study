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

