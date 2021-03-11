# Semantic segmentation
 - Image classification을 pixel 단위로 하는 것
 - 같은 class는 같은 segmentation으로 분류(같은 사람은 같은 색)
 ![image](https://user-images.githubusercontent.com/43736669/110401947-e1c6ab80-80bd-11eb-96d7-48651934a330.png)

## 활용 사례
![image](https://user-images.githubusercontent.com/43736669/110401989-f145f480-80bd-11eb-848f-43de49ffc504.png)
computational photography : 컴퓨터를 이용해 사진을 편집하는 것

## Fully Convolutional Networks
![image](https://user-images.githubusercontent.com/43736669/110402140-2f431880-80be-11eb-9f98-d7c350ee635a.png)
 - 첫 end-to-end 구조. 입력과 출력 pair를 통해 target task 해결
 - 입력과 출력의 해상도가 같음(기존 image classification 모델 에서는 마지막에 flatten 해서 안됨)

### Fully connected 와 Fully convolutional
 ![image](https://user-images.githubusercontent.com/43736669/110403651-d32dc380-80c0-11eb-800c-f81b4e7bb61f.png)
 - fully connected : fixed dimensional vector를 output으로 가짐. 공간 정보(spatial coordinates)를 고려하지 x
 - fully convolutional : 입력도 Activation map, 출력도 Activation map. Spatial coordinates를 유지. 각 픽셀마다 classification 결과를 출력
 
 ![image](https://user-images.githubusercontent.com/43736669/110403945-53ecbf80-80c1-11eb-8a0f-babb672eeb93.png)
  - 기존의 image classification에서의 flattening 은 공간 정보를 고려하지 못함.
 
 ![image](https://user-images.githubusercontent.com/43736669/110404103-9c0be200-80c1-11eb-8eda-c5cc1befda06.png)
  - 각 픽셀의 정보를 flattening 하는 개념으로 1x1 convolution 한다면, 공간 정보를 추출하는 것이 가능함.
  - 각 위치별로 classification 하는 것이 가능

 ![image](https://user-images.githubusercontent.com/43736669/110404402-205e6500-80c2-11eb-8cb0-3e0cc2a25e1c.png)
  - 이러한 작업을 거치면 해상도(resolution)가 필연적으로 낮아지게 됨(pooling, stride 등의 영향) -> upsampling 고려
 
 
### Upsampling
  - 일단은 작게 만들어서 receptive field는 최대한 키워 놓은 후(성능을 위해), 거의 마지막에 가서 upsampling으로 해상도를 맞춘다는 개념
  ![image](https://user-images.githubusercontent.com/43736669/110404655-9793f900-80c2-11eb-9762-0655287ccd60.png)

#### Transposed Convolution
  ![image](https://user-images.githubusercontent.com/43736669/110404749-c14d2000-80c2-11eb-9cf0-8efc05db5384.png)  
   - output size로 맞추면서 중첩되는 부분은 더함
  ![image](https://user-images.githubusercontent.com/43736669/110404902-0ffaba00-80c3-11eb-9876-6a34f0b62cb5.png)
   - 따라서 중첩되는 부분이 overlap 되는 문제를 신경써서 튜닝을 해야함(stride, convolution 크기 등 고려)
 
#### 이러한 문제를 해결한 Upsampling
![image](https://user-images.githubusercontent.com/43736669/110405136-71bb2400-80c3-11eb-9054-13602e65b66c.png)
 - 영상 처리 기법인 interpolation(NN, Bilinear)를 사용하며, 학습이 가능하도록 convolution까지 추가

### FC의 각 레이어의 특징
![image](https://user-images.githubusercontent.com/43736669/110405355-cced1680-80c3-11eb-8eb9-f63b150016f9.png)
 - 낮은 layer : receptive field size가 작음. 국지적이며 작은 차이에도 민감한 경향
 - 높은 layer : 해상도는 낮아지지만 큰 receptive field를 가지며 전반적이고 의미론적인 정보 포함
 - Semantic Segmentation에는 두 종류의 특징이 다 필요
  
 ![image](https://user-images.githubusercontent.com/43736669/110405505-0aea3a80-80c4-11eb-8b15-dc6e05e729fc.png)
 - 이 두 특징을 확보하기 위해 합침
 - 높은 곳에 있는 layer : upsampling 해서 해상도를 크게 만들어 layer들을 합침
 - 중간 단계 특징들을 합쳐서 쓰는 것이 큰 도움이 됨
 ![image](https://user-images.githubusercontent.com/43736669/110405727-5c92c500-80c4-11eb-944b-dbef99e0827c.png)

## Hypercolumns
 - 1x1 convolution, fully convolutional 보다는 낮은 layer의 정보와 높은 layer의 정보를 융합하는 것의 중요성을 강조
 ![image](https://user-images.githubusercontent.com/43736669/110405855-96fc6200-80c4-11eb-9e13-4e3e37bd0772.png)
 - 낮은 layer와 높은 layer를 해상도를 맞춰 쓰는 것을 제시
  
### overall architectiure
 ![image](https://user-images.githubusercontent.com/43736669/110405991-d1fe9580-80c4-11eb-8b15-22633b7db44c.png)

## U-Net
 - semantic segmentation breakthrought의 시작
 - Fully convolutional property 유지
 - 낮은 층 Feature와 높은 층 Feature를 skip connection을 통해 결합하는 것을 제시

### overall architecture
![image](https://user-images.githubusercontent.com/43736669/110406180-299d0100-80c5-11eb-8b12-2a4f86d32b5b.png)
![image](https://user-images.githubusercontent.com/43736669/110783310-9a9e0d80-82ab-11eb-8579-fd73b647cbf7.png)
- 먼저 input image에 대해 pooling을 통해 해상도를 나주고 채널 수를 늘림(receptive field 올림)
- 반복해서 작은 activation map을 구함(영상의 전반적인 정보가 잘 녹아있다고 가정)
![image](https://user-images.githubusercontent.com/43736669/110783438-ccaf6f80-82ab-11eb-9045-f9ed6d1ccb6c.png)
- decoding 과정. 단계별로 activation map의 해상도, 채널 size를 올려줌
- 낮은 층에 대칭으로 대응되는 layer와 동일한 size로 맞춰서 낮은 층의 activation map을 합쳐서 사용할 수 있도록 함
- 이후 skip connection으로 합침(concat)
- channel size는 줄어들고, 해상도는 커지게 됨
![image](https://user-images.githubusercontent.com/43736669/110783707-20ba5400-82ac-11eb-8d6c-c62fc1a69962.png)
- 낮은 layer에서 전달된 특징이 localized 된 정보를 줌
- 공간적인 정보(낮은 layer의 정보)를 뒤쪽 layer에 민감하게 전달
![image](https://user-images.githubusercontent.com/43736669/110783864-4e9f9880-82ac-11eb-9a6a-fb220c2bd9e9.png)
- activation map의 spatial size가 홀수라면 안 맞을 가능성이 있음
![image](https://user-images.githubusercontent.com/43736669/110784004-7b53b000-82ac-11eb-8a5e-a7b249a39f44.png)
![image](https://user-images.githubusercontent.com/43736669/110784053-89093580-82ac-11eb-8878-fdc6e15e13f5.png)
- upsampling을 위해 ConvTransposed2d를 사용(stride, kernel size 다 2라서 한칸씩 뛰면서 두칸씩 채워넣으므로 중첩이 안 생김)

## DeepLab
 - CRF 라는 후처리, Atrous Convolution의 사용
### CRFs
![image](https://user-images.githubusercontent.com/43736669/110784341-eb623600-82ac-11eb-9358-8949651ec1ce.png)
- 픽셀과 픽셀 사이의 관계를 이어주는 모델링(graph) 
- sementic segmention의 첫 output은 굉장히 blur된 값이 나오게 됨. 이를 해결하기 위해 출력 map과 이미지 경계선을 활용해서 score map이 경계에 잘 들어맞도록 확산 시켜줌. 반대로 background 또한 확산시켜(CRF iter) 물체에 경계에 잘 맞는 segmentation을 얻음
### Dilated convolution
![image](https://user-images.githubusercontent.com/43736669/110784668-4c8a0980-82ad-11eb-955d-ab20bc8dbfba.png)
### Depthwise convolution
![image](https://user-images.githubusercontent.com/43736669/110784741-6592ba80-82ad-11eb-8178-2cca0cb9683c.png)
- 기존 convolution은 하나의 activation 을 얻기 위해서 커널 전체가 채널 전체에 내적하여 하나의 값을 뽑음
- depthwise convoltion은 각 절차를 둘로 나눠서, 각 채널을 채널별 conv하고, 그 후 각 채널별 map을 1x1 conv
- convolution의 표현력은 유지되며, 계산량은 획기적으로 감소
### Deeplap v3
![image](https://user-images.githubusercontent.com/43736669/110785049-ce7a3280-82ad-11eb-843c-cd7f8cd28ccc.png) 
 - dilated convolution layer들 에서 더 큰 receptive field를 가지는 cnn을 적용해서 feature map을 구함
 - 다양한 rate의 conv들을 통해 multi scale을 처리 -> concat 후 1x1 conv : 다양한 물체의 크기를 고려한 모듈
 - decoder에서 low level feature과 pyramid pooling feature를 concat 후 upsample을 통해 segmentation 추출 

