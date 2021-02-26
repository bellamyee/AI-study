# 정점 표현 학습
## 정점 표현 학습이란
정점 표현 학습이란 그래프의 정점들을 벡터의 형태로 표현하는 것입니다.

- 정점 표현 학습은 정점 임베딩(Node Embedding)이라고 부름. 

- 정점 임베딩은 벡터 형태의 표현 그 자체를 의미 

- 정점이 표현되는 벡터 공간을 임베딩 공간이라고 함 

![image](https://user-images.githubusercontent.com/43736669/109259670-07db8880-7840-11eb-84d3-a5b2478bf743.png) 

정점 표현 학습이란 그래프의 정점들을 벡터의 형태로 표현하는 것

 - 입력은 그래프
 - 추력은 주어진 그래프의 각 정점 u에 대한 임베딩(벡터 표현)Zu 

![image](https://user-images.githubusercontent.com/43736669/109259758-38232700-7840-11eb-94ee-6aa335ed0ec1.png)

## 정점 표현 학습의 이유
정점 임베딩의 결과로 벡터 형태의 데이터를 위한 도구들(ML 도구들)을 그래프에도 적용 가능

## 정점 표현 학습의 목표
그래프에서의 정점 간 유사도를 임베딩 공간에서도 보존하는 것을 목표로 함

![image](https://user-images.githubusercontent.com/43736669/109259920-83d5d080-7840-11eb-990b-cb7c2bb684a4.png) 

임베딩 공간의 유사도로 내적을 사용 

![image](https://user-images.githubusercontent.com/43736669/109259981-a5cf5300-7840-11eb-8d90-1445972dcc8e.png) 

### 정점 임베딩의 두 단계 
 1) 그래프에서의 정점 유사도를 정의하는 단계
 2) 정의한 유사도를 보존하도록 정점 임베딩을 학습하는 단계 

# 인접성 기반 접근법
## 인접성 기반 접근법이란
두 정점이 인접(Adjacency)할 때 유사하다고 함 

두 정점 u와 v가 인접하다는 것은 둘을 직접 연결하는 간선(u,v)가 있음을 의미 

![image](https://user-images.githubusercontent.com/43736669/109260212-11b1bb80-7841-11eb-97e0-496f4e3b01e7.png)

인접성 기반 접근법의 Loss Function은 다음과 같음 

![image](https://user-images.githubusercontent.com/43736669/109260259-2a21d600-7841-11eb-906b-271f80c8a5a3.png)

## 인접성 기반 접근법의 한계
인접성만으로 유사도를 판단하는 것은 한계가 있음

![image](https://user-images.githubusercontent.com/43736669/109260432-766d1600-7841-11eb-867f-e886f05228bd.png)

위 표현에서 빨간색 정점과 파란색 정점은 다른 군집에 속하는 반면, 초록색 정점과 파란색 정점은 다른 군집에 속함 

- 인접성만을 고려하면, 두 경우의 유사도는 0으로 같음

# 거리/경로/중첩 기반 접근법
## 거리 기반 접근법
 - 두 정점 사이의 거리가 충분히 가까운 경우 유사하다고 간주. 

![image](https://user-images.githubusercontent.com/43736669/109261245-e6c86700-7842-11eb-8a32-11bafe12a988.png) 

## 경로 기반 접근법
 - 두 정점 사이의 경로가 많을수록 유사하다고 간주

![image](https://user-images.githubusercontent.com/43736669/109261847-de246080-7843-11eb-8547-5eb59fb55812.png)

## 중첩 기반 접근법 
 - 두 정점이 많은 이웃을 공유할 수록 유사하다고 간주
 
 ![image](https://user-images.githubusercontent.com/43736669/109261940-07dd8780-7844-11eb-9bf9-b7c38ea7de1c.png) 

 - 두 정점이 많은 이웃을 공유할수록 유사하다고 간주
 
 ![image](https://user-images.githubusercontent.com/43736669/109262001-22affc00-7844-11eb-8d3c-5c2656bca01c.png)

 ![image](https://user-images.githubusercontent.com/43736669/109262122-4ffcaa00-7844-11eb-91f2-a357f631ea1d.png)

# 임의보행 기반 접근법
## 임의보행 기반 접근법이란
- 한 정점에서 시작해서 임의보행을 할 때 다른 정점에 도달할 확률을 유사도로 간주 

![image](https://user-images.githubusercontent.com/43736669/109262747-6d7e4380-7845-11eb-89dd-e76de93aa45e.png)

임의보행 기반 접근법은 세 단계를 거침 

![image](https://user-images.githubusercontent.com/43736669/109262990-de256000-7845-11eb-90b6-ca422a49d729.png) 

어떻게 임베딩으로부터 도달 확률을 추정할까? 

![image](https://user-images.githubusercontent.com/43736669/109263057-fdbc8880-7845-11eb-8396-aae63ae26634.png)

추정한 도달 확률을 사용해 손실함수를 완성하고 이를 최소화하는 임베딩을 학습

![image](https://user-images.githubusercontent.com/43736669/109263137-17f66680-7846-11eb-907a-7d02c38ab2e9.png)

## DeepWalk

임의보행의 방법에 따라 DeepWalk와 Node2Vec이 구분됨

DeepWalk는 앞서 설명한 기본적인 임의보행을 사용. 현재 정점의 이웃 중 하나를 균일한 확률로 선택하는 이동하는 과정을 반복

## Node2Vec

Node2Vec은 2차 치우친 임의보행(Second-order Biased Random Walk)을 사용

현재 정점에서(v)와 직전에 머무렀던 정점(u)을 모두 고려하여 다음 정점을 선택

직전 정점 거리 기준으로 경우를 구분하여 차등적인 확률을 부여

![image](https://user-images.githubusercontent.com/43736669/109263438-97843580-7846-11eb-8c7c-0305da6bcd6d.png)

부여하는 확률에 따라 다른 종류의 임베딩을 얻음

![image](https://user-images.githubusercontent.com/43736669/109263516-bc78a880-7846-11eb-99ac-bd5681331ac8.png)

