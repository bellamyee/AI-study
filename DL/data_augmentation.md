# Data Augmentation
## Data Augmentation의 필요성
- 실제 세상의 데이터들(카메라로 찍힌 데이터들)은 모두 biased 됨(패턴화 됨). 실제 세상의 데이터와 괴리가 있음.
![image](https://user-images.githubusercontent.com/43736669/110342597-eadc5c00-806e-11eb-9647-8f951d3266b3.png)

- train data 는 real data와 다른 데이터다(단지 샘플된 데이터)
![image](https://user-images.githubusercontent.com/43736669/110342792-270fbc80-806f-11eb-9f8b-71f4765fca75.png)

- 일례로 밝은 색의 밝은 이미지로만 학습 하던 모델이 어두운 이미지를 보았을 떄 confused 될 수 있다.
![image](https://user-images.githubusercontent.com/43736669/110342886-40b10400-806f-11eb-93b0-d9150af73a66.png)

- 따라서 이런 train data와 real data간의 gap을 줄이기 위해 필요한 것이 data augmentation
![image](https://user-images.githubusercontent.com/43736669/110343070-75bd5680-806f-11eb-9f7d-1c29ffee2e63.png)

## Image data augmentation
 - transform : crop, shear, brightness, perspective, rotate 등등의 변환
 - training dataset을 real data distribution과 유사하게 만드는 것이 목표
 - 밝기 변경 : 일정 숫자를 더해주면 해결(혹은 scaling 등)
 ![image](https://user-images.githubusercontent.com/43736669/110343472-e06e9200-806f-11eb-9077-16e9be4fdb44.png)
 - rotate, flip 등도 간단하게 할 수 있음.
 ![image](https://user-images.githubusercontent.com/43736669/110343568-f7ad7f80-806f-11eb-8a4f-2d476b18308c.png)
 - crop 은 이미지의 part를 강조하여 학습 가능.
 ![image](https://user-images.githubusercontent.com/43736669/110343622-072cc880-8070-11eb-97c6-bf48f2d93be2.png)
 - affine(shear) transform : 선과 길이비, 평행성은 유지하며 변환. 변환의 기준이 되는 대응쌍을 기준으로 틀을 맞춘 변환 행렬이 나옴. 해당 matrix 기준으로 변환
 ![image](https://user-images.githubusercontent.com/43736669/110343764-29bee180-8070-11eb-9933-431d4b5b98ab.png)
 - cutMix : 이미지를 자르고 합성하는 것. label도 같은 비율에 따라 합성해줘야 함. 성능향상 + 물체의 위치를 더 정교하게 capture
 ![image](https://user-images.githubusercontent.com/43736669/110344282-ab167400-8070-11eb-9613-ae66253ab0c9.png)

## RandAugment
 - 여러 가지 가능한 augmentation을 조합해서 최적의 기법을 찾아내는 방법
 - random sample, apply, evluate해 최적의 조합을 찾아냄
 ![image](https://user-images.githubusercontent.com/43736669/110344591-fdf02b80-8070-11eb-935c-0bf93e89a9cc.png)
 
  
