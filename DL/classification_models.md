# Classification Models

## Brief History
![image](https://user-images.githubusercontent.com/43736669/110337466-4c013100-8069-11eb-923c-cd6591c0d62f.png)

## AlexNet
### Pre-AlexNet : LeNet
![image](https://user-images.githubusercontent.com/43736669/110338083-f416fa00-8069-11eb-9a78-ae354298cd87.png)

### LeNet과 AlexNet의 차이점
1) 크다(7 hidden layers, 605k neurons, 60 million parameters)
2) ImageNet data로 train
3) ReLU activation Func의 사용과 dropout technique

### Alexnet 구조
![image](https://user-images.githubusercontent.com/43736669/110338549-77d0e680-806a-11eb-886a-a29db2360b2f.png)
 
  GPU 메모리 문제로 두개를 이용하여 각각 계산하도록 하는 구조
  
![image](https://user-images.githubusercontent.com/43736669/110338850-d5fdc980-806a-11eb-85c0-5530e2eb9286.png)

 마지막 maxpool에서 dense layer로 가기 위해서는 vectorize가 필요
  1) average pooling 
  2) flattening (채택)
 
 ### LRN : Local Response Normalization
 
  - activation map에서 명암을 normalization 하는 역할을 함(현재는 사용하지 않음)
  - 최근 코드에서는 Batch Normalization으로 대체

 ### Convolution Filter
  - 최신 Network 구조에 비해 큰 conv filter size 채택
  - Receptive Field : CNN feature가 영향을 끼치는 input space
  
## VGGNET
### 특징
  ![image](https://user-images.githubusercontent.com/43736669/110340019-2590c500-806c-11eb-964c-dd383312cae8.png)
 
  - 깊이가 깊어짐, LRN 사용 X, 3x3 conv filter, 2x2 pooling만 사용  
  - fine tuning 시 다른 task로의 generalization이 잘 됨. 
  - 정리 : 더 깊고 심플한 구조. 더 나은 성능 
  
### 상세 구조
  - input layer : 224x224 RGB images, train image의 평균 RGB 값을 빼줌(normalization)  
  - feature layer : 3x3 conv layer를 deep 쌓음. 이 경우 filter 크기가 작음에도 큰 receptive field를 가질 수 있으며 parameter 수는 감소.  
  - classification layer : 3 FC layer. ReLU를 사용함

### 깊게 쌓는 것의 문제점
  - 점점 깊게 쌓을수록 Gradient vanishing / exploding=
  - 계산 복잡도 문제
  - Overfitting(X) Degradation problem(O)

## GoogLeNet

### Inception module
![image](https://user-images.githubusercontent.com/43736669/110399046-6f9f9800-80b8-11eb-8b76-875b9edd9dd2.png)

- 하나의 layer에서 여러 convolution filter를 적용해 output을 concat
- network size가 커지면 computational resources를 많이 잡아먹음 -> 1x1 convolutions 사용(Dimension reduce)
- channel dimension을 바꿔줌(심지어 max pooling에서도)

### 1x1 convolutions
 activation map에서 각 픽셀에 해당하는 채널 축으로 값들을 쌓아서 filter와 내적한 후 m개의 채널로 차원 축소(차원간  convolution?). 각 픽셀에서 채널 수만 조절(사진에선 4->2)
 ![image](https://user-images.githubusercontent.com/43736669/110399728-a6c27900-80b9-11eb-87a1-c08b5839d221.png)

### GoogLeNet architecture
![image](https://user-images.githubusercontent.com/43736669/110400097-631c3f00-80ba-11eb-87dd-ffbea2131126.png)
-inception module을 여러 층 쌓고, 중간중간 gradient를 주입하는 auxiliary classifier 사용

## ResNet
- deeper network를 쌓으려고 함
### degradation problem
- network가 깊어질수록, 성능이 안 좋아지는 이유가 overfitting 때문일까? no. 최적화 문제(overfitting 때문이라면 train error가 deep 할수록 적어야 함)
- optimization 문제!
![image](https://user-images.githubusercontent.com/43736669/110400540-21d85f00-80bb-11eb-8033-9bfa0c70d121.png)

### residual function
![image](https://user-images.githubusercontent.com/43736669/110459042-d0a68a80-810f-11eb-91b1-245f8d14ee9c.png)
 - X to H(x) 관계를 학습할 때 중간 층이 deep 하면 학습하기가 어려워 residual function 이용해 target function 학습
 - vanashing gradient problem 해결
 - shortcut connection
![image](https://user-images.githubusercontent.com/43736669/110459367-3e52b680-8110-11eb-80f0-2a660b2d5fd1.png)
 - n개의 residual block을 사용하는 경우 모든 residual path 경우의 수는 2^n개가 됨(스위치 껐다 켰다 하는거니까..)
 - 굉장히 복잡한 mapping을 학습할 수 있음
 
 ### overall architecture
![image](https://user-images.githubusercontent.com/43736669/110464505-8e347c00-8116-11eb-9cdb-137ae45201c0.png)

## DenseNet
 - ResNet과 유사하지만, 더하기 연산 대신 channel 방향으로 concat 
 ![image](https://user-images.githubusercontent.com/43736669/110465538-dc964a80-8117-11eb-826a-6185847b3818.png)

## SENet
 - 채널 간 관계 모델링. attention 적용
 - squeeze와 excitation을 통해 attention
 - squeeze : global avg pooling 을 통해 각 채널의 공간 정보를 없애고 분포를 구하게 됨
 - excitation : 채널 간의 연관성을 고려 -> attention score 생성
 - 이렇게 나온 attention으로 입력 attention과 weight를 통해 activation을 rescaling(중요한 값을 강조)
 ![image](https://user-images.githubusercontent.com/43736669/110465645-08b1cb80-8118-11eb-96f9-7d6c25c4587f.png)
 
## EfficientNet
 - 채널축을 늘리고(DenseNet), 깊이를 깊게 하고(ResNet), input resolution을 큰걸 넣어주고
 - 위 factor들을 분배하는 전략 구상
 ![image](https://user-images.githubusercontent.com/43736669/110466321-f84e2080-8118-11eb-924b-36050c2a013d.png)
 - [self-trainning](https://github.com/JeonghwanLee1/AI-study/blob/main/DL/pretrained.md)
 
 


