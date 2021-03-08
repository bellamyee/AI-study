# Transfer Learning
- 충분한 양의 high-quality의 데이터셋과 label을 모으는 것이 어렵다. 이를 해결하기 위해 나온 기술
- 기존 pre-trained knowledge를 활용하여 새 task에 적용하는 것
- idea : 한 데이터셋에서 배운 지식중 다른 데이터셋에 적용할 수 있는 정보들이 있을 수 있다!

## 필요한 Layer만 학습하고, 나머지는 freeze하는 방식
![image](https://user-images.githubusercontent.com/43736669/110345827-507e1780-8072-11eb-9735-a43761da2da3.png)
- 기존 모델의 마지막 layer만 제거하고 새로 FC layer만 추가하여 학습하는 방식. 앞의 Conv layers의 weight는 기존 것으로 고정.
- 적은 데이터로도 학습 가능(parameter 수가 감소)

## 전체 model을 학습하는 방법
![image](https://user-images.githubusercontent.com/43736669/110346697-25e08e80-8073-11eb-94e1-7974bdb8d1ab.png)
- 앞분은 learning rate를 작게 해서 update하고, 새로 생긴 부분은 빠르게 학습하는 것
- 첫 번째 방법에 비해 많은 시간이 걸릴 수도 있음

# Knowledge distillation
- 큰 모델에서 작은 모델로 지식을 전달하는 것(Teacher-student learning)
- 원래는 모델 압축에 자주 사용되었으나, pseudo-labeling(label 없는 데이터셋을 라벨링 하는 것)에도 사용되기 시작
![image](https://user-images.githubusercontent.com/43736669/110347159-aef7c580-8073-11eb-88ab-300b25a2ead6.png)

## teacher-student network structure
 - student는 teacher의 output을 흉내내는 방향으로 학습.
 - unlabeled data를 통해서 학습할 수 있으므로 unsupervised learning임 
![image](https://user-images.githubusercontent.com/43736669/110347290-ce8eee00-8073-11eb-8ffa-33b9a3e22507.png)
 - 둘의 output을 비교하여, KL div.Loss를 최소화하는 방향으로 학습(둘의 출력 distribution을 비슷하게)

 - label이 존재하는 데이터라면, 아래와 같이 learning
 ![image](https://user-images.githubusercontent.com/43736669/110347631-27f71d00-8074-11eb-8a4f-ece6a7c2a06d.png)
 - soft label과 Temperture softmax 사용
 - student loss와 distillation loss 사용

### Hard Label vs Soft Label
 - Hard label : 1 or 0 ( one - hot ). 실제 데이터셋이 가지고 있는 label
 - Soft label : model의 softmax output(실수 벡터). 모델의 knowledge
 ![image](https://user-images.githubusercontent.com/43736669/110348038-91772b80-8074-11eb-9988-4049466f7d4f.png)

### Temperature(T)
 - 기존의 softmax함수는 입력의 값을 극단적으로 벌려주는 역할을 함(Hard prediction).
 - 하지만 입력을 큰 값(T)으로 나누어주게 된다면 출력의 차이를 줄어들게 됨(Soft prediction).
 - 극단적으로 0과 1에 가까운 값보다는(하나가 1이되면 나머지는 0에 가까운 값들이 됨) 분포를 더 잘 알 수 있는(정보를 많이 가지고 있는) 값을 사용하기 위해 
 ![image](https://user-images.githubusercontent.com/43736669/110348464-077b9280-8075-11eb-8382-1d6abbe23941.png)

### Student loss와 Distillation loss
 ![image](https://user-images.githubusercontent.com/43736669/110348774-5a554a00-8075-11eb-8b81-d2b43bdf8e43.png)

# Self-trainning
## Semi-supervised Learning 
 - labeled dataset + unlabeled dataset으로 학습하는 방법
 ![image](https://user-images.githubusercontent.com/43736669/110349530-24649580-8076-11eb-9bf2-d321f96bd0b5.png)
- labeled로 모델 학습 -> 모델로 unlabeled 예측 후 pseudo labeled 생성 -> labeled+pseudo labeled로 train 

## Self-trainning
 - Augmentation + Teacher-Student + Semi-supervised Learning
 
 ![image](https://user-images.githubusercontent.com/43736669/110349831-73aac600-8076-11eb-979f-49fd59d65322.png)
 
 1) ImageNet으로 Teacher Model 학습
 2) Teacher model로 300M unlabeled data를 pseudo-label
 3) 두 데이터를 합쳐서 student model(점점 커짐) 학습(RandAugment 이용)
 4) 이전 Teacher Network를 최근 학습된 Student 모델로 최신화
 5) 반복

![image](https://user-images.githubusercontent.com/43736669/110350145-c5535080-8076-11eb-9224-beee9d246e66.png)
 - 매 round마다 더 큰 student 모델 사용(knowledge distillation과는 반대)

