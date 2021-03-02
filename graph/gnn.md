# 그래프 신경망
## 그래프 신경망 구조
#### 그래프 신경망은 정점의 속성 정보를 입력으로 받음 
![image](https://user-images.githubusercontent.com/43736669/109577620-3fe11500-7b39-11eb-8e02-d48f48b69198.png)
#### 정점의 속성의 예시는 다음과 같음
 - 온라인 소셜 네트워크에서 용자의 지역, 성별, 연령, 프로필 사진 등
 - 논문 인용 그래프에서 논문에 사용된 키워드에 대한 원-핫 벡터
 - PageRank 등의 정점 중심성, 군집 계수(Clustering Coefficient) 등
#### 그래프 신경망은 이웃 정점들의 정보를 집계하는 과정을 반복하여 임베딩을 얻음
예시에서 해당 점점의 임베딩을 얻기 위해 이웃들 그리고 이웃의 이웃들의 정보를 집계  
![image](https://user-images.githubusercontent.com/43736669/109577806-92223600-7b39-11eb-8a28-831c6ca7f332.png)  
- 각 집계 단계를 층(Layer)이라고 부르고, 각 층마다 임베딩을 얻음  
- 각 층에서는 이웃들의 이전 층 임베딩을 집계하여 새로운 임베딩을 얻음  
- 0번 층, 즉 입력 층의 임베딩으로는 정점의 속성 벡터를 사용  
![image](https://user-images.githubusercontent.com/43736669/109577904-c3026b00-7b39-11eb-8100-791416aae14d.png)  
![image](https://user-images.githubusercontent.com/43736669/109577943-d4e40e00-7b39-11eb-94d9-608c96773a66.png)
#### 서로 다른 대상 정점간에도 층 별 집계 함수는 공유 
![image](https://user-images.githubusercontent.com/43736669/109577995-eb8a6500-7b39-11eb-8613-fbf3d8b4e9bf.png)
#### 서로 다른 구조에서의 그래프 처리를 위한 집계 함수?
![image](https://user-images.githubusercontent.com/43736669/109578061-03fa7f80-7b3a-11eb-98ec-7027b926a2a1.png)
![image](https://user-images.githubusercontent.com/43736669/109578113-18d71300-7b3a-11eb-8e23-201b0d680db9.png)
![image](https://user-images.githubusercontent.com/43736669/109578134-212f4e00-7b3a-11eb-8b46-fe01b9398c31.png)
## 그래프 신경망의 학습 
![image](https://user-images.githubusercontent.com/43736669/109578247-2b514c80-7b3a-11eb-8b79-1d76231bf608.png)
- 손실함수의 정의 : 정점 간 거리를 보존하는 것을 목표로
- 변환식 정점 임베딩에서처럼 그래프에서의 정점간 거리를 보존하는 것을 목표로 할 수 있음. 만약, 인접성을 기반으로 유사도를 정의한다면, 손실 함수는 다음과 같음
![image](https://user-images.githubusercontent.com/43736669/109578378-6bb0ca80-7b3a-11eb-88e7-7f5ccb54f1a4.png)
#### 후속 과제(Downstream Task)의 손실함수를 이용한 End-to-End 학습도 가능
![image](https://user-images.githubusercontent.com/43736669/109579299-f80fbd00-7b3b-11eb-9028-ae0730da4687.png)
![image](https://user-images.githubusercontent.com/43736669/109579331-09f16000-7b3c-11eb-80d2-258234279379.png)
![image](https://user-images.githubusercontent.com/43736669/109579370-1d9cc680-7b3c-11eb-94db-4b96cda6e805.png)
![image](https://user-images.githubusercontent.com/43736669/109580878-b2a0bf00-7b3e-11eb-9c51-9c93bca8b7e9.png)
#### 학습 순서
![image](https://user-images.githubusercontent.com/43736669/109580938-ce0bca00-7b3e-11eb-9860-1e37a9cb69bb.png)
![image](https://user-images.githubusercontent.com/43736669/109580959-dc59e600-7b3e-11eb-9810-31c9fbf1d3bf.png)
## 그래프 신경망의 활용
#### 학습된 신경망을 적용해 학습에 사용되지 않은 정점의 임베딩을 얻을 수 있음
![image](https://user-images.githubusercontent.com/43736669/109581015-f72c5a80-7b3e-11eb-87b3-c97169b07d32.png)
#### 마찬가지로, 학습 이후에 추가된 정점의 임베딩도 얻을 수 있음
![image](https://user-images.githubusercontent.com/43736669/109581062-0f9c7500-7b3f-11eb-910e-13d789a933de.png)
#### 학습된 그래프 신경망을 새로운 그래프에 적용할 수도 있음
![image](https://user-images.githubusercontent.com/43736669/109581120-3064ca80-7b3f-11eb-8b61-87b30f1c60d5.png)

# 그래프 신경망 변형

## 그래프 합성곱 신경망
![image](https://user-images.githubusercontent.com/43736669/109581174-483c4e80-7b3f-11eb-9e54-6fa391bbd913.png)
![image](https://user-images.githubusercontent.com/43736669/109581240-50948980-7b3f-11eb-97c2-2b075ea21a84.png)

## GraphSAGE
![image](https://user-images.githubusercontent.com/43736669/109581258-5ab68800-7b3f-11eb-9b6c-9deb6dc317f4.png)
![image](https://user-images.githubusercontent.com/43736669/109581299-673ae080-7b3f-11eb-8a35-84e06db50f7f.png)
