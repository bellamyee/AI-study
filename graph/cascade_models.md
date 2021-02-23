# 선형 임계치 모델(Linear Threshold Model)
 - 주변 사람들의 의사결정을 고려하여 각자 의사결정을 내리는 경우 의사결정 기반의 전파 모형을 사횽
## 추상화
 - 친구 관계의 두사람 u,v 를 가정할 때 두 개의 호환되지 않는 기술 A, B 중 하나를 선택해야함
 - 둘 다 A 기술, B 기술을 사용할 경우 행복이 a, b 만큼 증가. 다른 기술의 경우 증가하지 않음 
 ![image](https://user-images.githubusercontent.com/43736669/108803329-c2b81c00-75dd-11eb-9148-72fc2eb3bee1.png) 
 - 여러 사람과 관계를 맺으므로, 네트워크 상에서 발생하는 행복을 고려
 ![image](https://user-images.githubusercontent.com/43736669/108803379-e24f4480-75dd-11eb-94fc-2cc6e0d02af2.png)
 - 여기서 행복이 최대화 되려면, 다음과 같이 결정함
 ![image](https://user-images.githubusercontent.com/43736669/108803445-0448c700-75de-11eb-9a36-db91cbb7d1a3.png) 
 ![image](https://user-images.githubusercontent.com/43736669/108803490-24788600-75de-11eb-95a6-e1f6fba19f51.png) 
## 선형 임계치 모델로의 일반화
 - 위 모형을 선형 임계치 모델(Lienar Threshold Model) 이라고 함
 - 각 정점은 이웃 중 A를 선택한 비율이 임계치 q를 넘을 때만 A를 선택
  
 - 모두 B를 사용하는 상황에서, 처음 A를 사용하는 얼리어답터들이 있다고 가정,
 - Seed Set이라고 불리는 얼리 어답터들은 항상 A를 고수한다고 가정.
 ![image](https://user-images.githubusercontent.com/43736669/108803622-7b7e5b00-75de-11eb-8e69-0d741def2b6d.png)
 ![image](https://user-images.githubusercontent.com/43736669/108803670-8fc25800-75de-11eb-81fd-6b17f4083b67.png)
 ![image](https://user-images.githubusercontent.com/43736669/108803707-ac5e9000-75de-11eb-8b64-e2609a0b141a.png)
 ![image](https://user-images.githubusercontent.com/43736669/108803747-c7c99b00-75de-11eb-939b-bf333a33dc92.png)
 ![image](https://user-images.githubusercontent.com/43736669/108803766-d4e68a00-75de-11eb-8a20-507de158225c.png)

# 확률적 전파 모델
- 코로나의 전파 과정을 수학적으로 추상화한다면, 의사 결정 기반 모형은 적합하지 않음(의사결정이 없기 때문).
- 따라서 이 경우 확률적 전파 모형을 고려해야 함
## 독립 전파 모형(Independent Cascade Model)
![image](https://user-images.githubusercontent.com/43736669/108803964-60f8b180-75df-11eb-98c9-b50c49015a12.png)
- 위 경우 첫 감염자들을 시드 집합(Seed Set)이라고 부름. 더 이상 새로운 감염자가 없을 때 종료

# 바이럴 마케팅과 전파 최대화
## 바이럴 마케팅
### 바이럴 마케팅이란?
 - 소비자들로 하여금 상품에 대한 긍정적인 입소문을 내게 하는 기법
 - 소문의 시작점이 중요. 입소문이 전파되는 범위가 영향을 받기 때문 => 소셜 인플루언서

## 전파 최대화
 - 시드 집합이 전파 크기에 많은 영향을 미침.
 ![image](https://user-images.githubusercontent.com/43736669/108804102-b634c300-75df-11eb-9958-8eb7e11887c9.png)
 ![image](https://user-images.githubusercontent.com/43736669/108804193-eb411580-75df-11eb-8781-27949b8a87c0.png)
 - 그래프, 전파 모형, 시드 집합의 크기가 주어졌을 때 시드 집합을 찾는 문제를 젚나 최대화 문제(Influence Maximization)라고 함 
 - 하지만 굉장히 어려운 문제
 ![image](https://user-images.githubusercontent.com/43736669/108804240-162b6980-75e0-11eb-8771-ee335529d608.png)

## 정점 중심성 휴리스틱
 - 시드 집합의 크기가 k개로 고정되어 있을 때, 정점의 중심성(Node Centrality)이 높은 순으로 k개 정점 선택하는 방법
 - 정점 중심성으로는 페이지랭크 점수, 연결 중심성, 근접 중심성, 매개 중심성
 - 최고의 시드집합을 찾는다는 보장은 x
 
## 탐욕 알고리즘
 - Greedy Algorithm 역시 많이 사용됨.
 ![image](https://user-images.githubusercontent.com/43736669/108804389-7b7f5a80-75e0-11eb-820f-598c95e83425.png)
 ![image](https://user-images.githubusercontent.com/43736669/108804358-65719a00-75e0-11eb-98a6-7c26c267c395.png)
 ![image](https://user-images.githubusercontent.com/43736669/108804377-715d5c00-75e0-11eb-8bb1-44ad2ecfd766.png)
