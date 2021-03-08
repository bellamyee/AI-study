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
  
  
