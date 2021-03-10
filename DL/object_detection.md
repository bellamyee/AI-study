# Object detection
## Classification + Box Localization
![image](https://user-images.githubusercontent.com/43736669/110581192-6512fa80-81ad-11eb-9e2c-5da825a0cc16.png)
- Autonomous driving, OCR 등에 활용

## Two-stage detector
### 과거의 object detection
![image](https://user-images.githubusercontent.com/43736669/110581259-8aa00400-81ad-11eb-9036-ac45a1e79e6a.png)
- 영상의 경계선을 찾아서 모델링(사람의 직관과 유사)
- 경계선의 방향을 추출해서 feature 추출

### Selective search
 - 사람이나 특정 물체 뿐 아니라 다양한 물체 후보군에 대해 bounding box 제안
 - 영상을 잘게 분할 먼저 함(over-segmentation)
 - 비슷한 영역으로 합침(반복)
 - 큰 segmentation을 포함하는 bounding box를 후보군으로 사용
 ![image](https://user-images.githubusercontent.com/43736669/110581565-20d42a00-81ae-11eb-9a0a-bf627b90c3d6.png)

### R-CNN
 ![image](https://user-images.githubusercontent.com/43736669/110581603-38131780-81ae-11eb-9ec6-fe8ebe9a42bf.png)
 - 영상에 region proposals를 구함(selective search 등 이용)
 - image classification에 적절한 size로 warping 해줌
 - CNN에 넣고 classification
 - pretrained 되어 있는 모델을 사용하고, 마지막 층의 SVM만 학습
 - 속도가 느림. hand-design algorithm(selective search) 사용으로 성능 향상의 한계가 있음
 
### Faster R-CNN
 영상 전체에 대한 feature들을 한번에 추출 -> 여러 object들을 추출할 수 있게 함
 ![image](https://user-images.githubusercontent.com/43736669/110581919-bff92180-81ae-11eb-99cc-15fdfc5e3667.png)
 1. original image 에서 convolution feature map 생성
 2. RoI pooling : 한번 뽑아놓은 feature를 재활용 하기위해. Region proposal 에서 제시한 boundary로 원본 feature을 projection 해서 pooling
 3. bounding box regression, classification task.
 - region proposal algorithm 을 NN 형태로 대체
 - 모든 part가 NN 기반으로 된 최초의 Object Detection 모델
 
#### IoU
 두 영역의 ovelap을 측정
 ![image](https://user-images.githubusercontent.com/43736669/110582552-b91ede80-81af-11eb-91e9-4ec84dd466a8.png)

#### Faster R-CNN 의 region proposal
![image](https://user-images.githubusercontent.com/43736669/110582628-d18ef900-81af-11eb-9fd7-cc7784ebf4ab.png)
 - Anchor Box : 각 위치에서 발생할 것 같은 box를 미리 정해놓은 후보군
 - Ground Truth 기반 IoU 측정. Object와 아닌 부분으로 나누어 loss 측정
 
 #### Faster R-CNN 의 특징
![image](https://user-images.githubusercontent.com/43736669/110582874-2fbbdc00-81b0-11eb-9db2-17315a9a4004.png)
 - selective Search 대신 Network(RPN) Module 제안
 - Feature을 미리 뽑아놓고 RPN 기반의 proposal을 이용하여 RoI pooling 수행

 #### RPN
 ![image](https://user-images.githubusercontent.com/43736669/110583025-6560c500-81b0-11eb-9ce2-028f50e9724d.png)
 - Feature Map 관점에서 Fully convolution, sliding window을 이용하여 매 위치마다 K개의 anchor box(미리 정해놓은) 고려
 - 2k개의 classification(object or not) score, 4k 개(x,y,높이,너비) 의 bound box의 regression output
 - 적당한 량의 anchor box를 만들어 놓고, 더 detail 하게는 regression 으로 해결 
 - classification loss, regression loss 둘 다 사용
 
 #### NMS
 - 너무 많이 겹쳐진 boxes 생성. 이를 효과적으로 필터링 및 스크리닝 하기 위한 방법
 ![image](https://user-images.githubusercontent.com/43736669/110583435-094a7080-81b1-11eb-8dc9-044249b25114.png)

 ### R-CNN Family summary
 ![image](https://user-images.githubusercontent.com/43736669/110583609-4a428500-81b1-11eb-9d6b-7990414b1627.png)
 
 ## Single-stage Detector
 ### One-stage vs two-stage
 ![image](https://user-images.githubusercontent.com/43736669/110583848-aa392b80-81b1-11eb-8314-299043e1b9d3.png)
 - 정확도를 조금 포기하고 속도를 얻음(real-time detection)
 - RoI를 포기하여 빠른 속도

 ### YOLO 
 ![image](https://user-images.githubusercontent.com/43736669/110583993-deace780-81b1-11eb-9292-6c6cd7137222.png)
 1) input image를 grid로 나눔
 2) 각 grid에 대해 4개의 좌표, confidence score, class score를 예측
 
 #### Train
 ![image](https://user-images.githubusercontent.com/43736669/110584129-161b9400-81b2-11eb-8f95-2439b1a11f44.png)
 -faster R-CNN과 유사
 
 #### Architecture
 ![image](https://user-images.githubusercontent.com/43736669/110584181-2895cd80-81b2-11eb-8113-79c49c8d88a8.png)
  - 최종 output은 7 by 7 * 30 channel (B = 2, C = 20)
  - 이 경우 grid(S) = 7. 이 수치가 마지막 layer의 해상도

 ### Single Shot Multibox Detector(SSD)
  - YOLO는 맨 마지막 layer에서 pred를 하기 때문에 localized에 약함
  - 이를 보완하기 위해 나옴
![image](https://user-images.githubusercontent.com/43736669/110584452-9510cc80-81b2-11eb-987f-80963638e128.png)
  - 각 feature map 마다 해상도에 적정한 bounding box의 크기들을 가지게 함(다양한 bounding box shape 고려 가능)
 #### 구조
 ![image](https://user-images.githubusercontent.com/43736669/110587436-0d798c80-81b7-11eb-94f5-71f43503d22e.png)
 
 ## Two-stage detector vs One-stage detector
 ### Focal loss
 ![image](https://user-images.githubusercontent.com/43736669/110587910-98f31d80-81b7-11eb-8bcc-4e2929dc9182.png)
  - Class imbalance : single stage는 RoI가 없다 보니 모든 영역에 대해 loss가 계산된다. 
 이를 해결하기 위해 Focal loss 사용
 ![image](https://user-images.githubusercontent.com/43736669/110588045-cd66d980-81b7-11eb-944b-5f824d54c896.png)
  - 앞에 확률 term 사용(1-pt) : 잘 맞춘 애들은 더 낮은 loss, 반대는 더 sharp 한 loss
  - 각 지점에서 gradient를 생각해야함(gamma가 클수록 정답에 먼 곳에서 더 sharp, 가까운곳에서 0에 가까운 grad)

 ## RetinaNet
 ![image](https://user-images.githubusercontent.com/43736669/110588371-48c88b00-81b8-11eb-9aeb-0859f2daa2b7.png)
  - U-Net과 유사한 구조
  - low level의 특징 layer, high level 특징 layer의 특징을 가지면서도 잘 넘겨주기 위해 이런 구조 채택(중간중간 넘겨줌)
  - class head와 box head 를 따로 구성해서 classification과 box regression을 dense하게 따로 시행
 
 # Detection with transformer
  ![image](https://user-images.githubusercontent.com/43736669/110588642-a5c44100-81b8-11eb-9e84-05ba86e7d905.png)
 
 ## DETR
  ![image](https://user-images.githubusercontent.com/43736669/110588684-b7a5e400-81b8-11eb-86ab-f7b44f6ff144.png)
  - encoder로 특징 추출ㄹ 후 decoder로 각각 넣어줌
  - transformer에 object quueries가 질의를 함(이 위치에 해당하는 object가 뭐임?)
  - 파싱되어서 나옴
 
 

