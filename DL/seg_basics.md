# Segmentation 개요  
## Sementic Segmentation과 Instance segmentation  
![image](https://user-images.githubusercontent.com/43736669/116040667-460df080-a6a7-11eb-8669-c38b6e92279a.png)

## Sementic Segmentation과 다른 분야 비교  
![image](https://user-images.githubusercontent.com/43736669/116040837-7786bc00-a6a7-11eb-9e34-c54e19fc9753.png)
- localization : class와 위치 정보 포함  
- object detection : 다중 객체 탐지  
- image segmentation : 픽셀마다 class로 분류  

## Sementic Segmentation 활용 분야  
![image](https://user-images.githubusercontent.com/43736669/116040910-8d947c80-a6a7-11eb-810f-91e082840b94.png)

## 딥 러닝을 이용한 Segmentation FCN
![image](https://user-images.githubusercontent.com/43736669/116041206-e82dd880-a6a7-11eb-8e20-07e1e8dea7d1.png)
1. VGGNet을 Backbone으로 사용
2. VGGNet의 FC(nn.linear)를 Convolution으로 대체
3. Transposed Convolution을 사용해 Pixel-Wise Prediction 수행

### VGG의 FC Layer를 Convolution으로 대체한 이유
![image](https://user-images.githubusercontent.com/43736669/116041450-2deaa100-a6a8-11eb-876c-064a2c21abab.png)  
![image](https://user-images.githubusercontent.com/43736669/116041510-3f33ad80-a6a8-11eb-98dd-a585bbddf700.png)
![image](https://user-images.githubusercontent.com/43736669/116041628-638f8a00-a6a8-11eb-8f6a-f991a27c712a.png)

### Transposed Convolution  
#### VGGNet 구조  
![image](https://user-images.githubusercontent.com/43736669/116041791-9cc7fa00-a6a8-11eb-8507-4fc2db4b5f7c.png)
- 해당 구조에서 Output이 input과 동일한 크기가 되어야 하는데, 이때 사용하는 upsample 기법이 transposed convolution  
#### Transposed Convolution 이란?(=Deconvolution, Upsampling)  
![image](https://user-images.githubusercontent.com/43736669/116042012-e4e71c80-a6a8-11eb-83e6-d4adc6cfa42c.png)
- Convolution 값이 backprop phase에서 학습됨.  
![image](https://user-images.githubusercontent.com/43736669/116042064-f4666580-a6a8-11eb-8a05-ad721f90360f.png)
![image](https://user-images.githubusercontent.com/43736669/116042117-0516db80-a6a9-11eb-8763-7f9e3b545a48.png)
![image](https://user-images.githubusercontent.com/43736669/116042201-195ad880-a6a9-11eb-9ba5-d675de91d364.png)
- 만약 5x5 output을 만들고 싶다면, stride를 2로 하면 됨  
![image](https://user-images.githubusercontent.com/43736669/116042285-30012f80-a6a9-11eb-9d19-c55249680ebd.png)

### FCN의 구현  
![image](https://user-images.githubusercontent.com/43736669/116042797-cd5c6380-a6a9-11eb-948e-6f48af0d3226.png)  
- convolution+ReLU  
![image](https://user-images.githubusercontent.com/43736669/116042850-de0cd980-a6a9-11eb-9ea9-0eb6028ab830.png)  
- Fully-Convolutional(1x1 이지만 원 논문에서는 7x7)  
![image](https://user-images.githubusercontent.com/43736669/116042933-fb41a800-a6a9-11eb-943d-d8af634e322f.png)  
![image](https://user-images.githubusercontent.com/43736669/116043006-157b8600-a6aa-11eb-8b4a-f1a2db28619a.png)
- 32배로 줄어든 이미지
![image](https://user-images.githubusercontent.com/43736669/116043091-2e843700-a6aa-11eb-95e5-6464ac5293db.png)
- upsample(32x)

### FCN 한계
![image](https://user-images.githubusercontent.com/43736669/116043180-4b206f00-a6aa-11eb-97a8-434d329c5e17.png)
- 32배만큼 줄인 이미지를 다시 늘려 늘릴 경우 매우 뭉뚱그려진 이미지가 나옴
- Stride 줄일 필요가 있다!

### 성능 향상(한계 극복) 기법(FCN16s)
![image](https://user-images.githubusercontent.com/43736669/116043285-6ee3b500-a6aa-11eb-912b-4cd86909c2d8.png)
- Skip connection 이용
- Deconvolution을 다층으로 쌓음
- => Maxpooling에 의해 잃어버린 정보를 복원, Upsample size를 줄여주기에 좀 더 효율적인 이미지 복원이 가능

### 실 구현(FCN16s)
![image](https://user-images.githubusercontent.com/43736669/116043478-ab171580-a6aa-11eb-851a-980e62686ad8.png)
![image](https://user-images.githubusercontent.com/43736669/116043503-b36f5080-a6aa-11eb-97f2-ab9f9a1d07da.png)
![image](https://user-images.githubusercontent.com/43736669/116043578-cf72f200-a6aa-11eb-979e-91dd47e76f84.png)
![image](https://user-images.githubusercontent.com/43736669/116043612-db5eb400-a6aa-11eb-8573-3116d1324707.png)
![image](https://user-images.githubusercontent.com/43736669/116043640-e285c200-a6aa-11eb-8d32-3c671e5a89a9.png)

### FCN8s
- Pool3 layer의 정보도 가져옴
- Deconv를 한층 더 깊게
![image](https://user-images.githubusercontent.com/43736669/116043790-1234ca00-a6ab-11eb-8f28-f3c7ba8b1d70.png)
![image](https://user-images.githubusercontent.com/43736669/116043819-1a8d0500-a6ab-11eb-9737-b52a40763a4a.png)

### 모델 비교
![image](https://user-images.githubusercontent.com/43736669/116043866-2a0c4e00-a6ab-11eb-81e3-2659f94c9db5.png)

# Segmentation 평가 지표
## Pixel Accuracy
![image](https://user-images.githubusercontent.com/43736669/116043959-4d36fd80-a6ab-11eb-99bb-2528370d595d.png)
## Mean IoU
![image](https://user-images.githubusercontent.com/43736669/116043999-59bb5600-a6ab-11eb-9905-502515de114d.png)
![image](https://user-images.githubusercontent.com/43736669/116044039-68097200-a6ab-11eb-91e3-62e0c856f963.png)

