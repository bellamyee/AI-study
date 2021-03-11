# Instance segmentation
## Mask R-CNN
 ![image](https://user-images.githubusercontent.com/43736669/110772060-8e5f8380-829e-11eb-9a12-e2362970ec2a.png)
 -  기존 Faster R-CNN 의 업그레이드 모델
 -  기존 RoI pooling은 정수 좌표만 지원했으나, mask R-CNN 에서는 RoI Align이라는 새로운 layer를 지원하여 소수점 레벨의 pooling 지원
 -  기존의 head(classification, box)들 옆에 mask branch를 추가. 80개의 class 별로 binary classification 생성
 -  classification head의 결과를 이용하여 아래의 mask 참조

## Summary of R-CNN family
 ![image](https://user-images.githubusercontent.com/43736669/110772745-4db43a00-829f-11eb-93cb-3c5797e6946e.png)

## YOLACT 
 - real time으로 segmentation이 가능한 모델(single stage 구조)
 ![image](https://user-images.githubusercontent.com/43736669/110772920-7e946f00-829f-11eb-8d72-14e4993e69a1.png)
 - 고해상도의 Feature들 사용
 - Mask의 protype들을 사용(Mask R-CNN은 80개의 모든 클래스에 대해 마스크 생성후 참조). Mask는 아니지만 Mask를 생성할 수 있는 기본적인 컴포넌트 생성
 - Prediction Head에서 각 detection에 대해서 protype을 잘 합성하기 위한 계수들 생성
 - 각 detection에 대해서 protype들을 weighted sum 해서 mask map 생성
 - Mask를 효율적으로 생성하기 위해 prototype 개수를 적당히 작게 설정하고 그것의 선형 결합으로 다양한 mask를 생성하는게 key point

### YolactEdge
![image](https://user-images.githubusercontent.com/43736669/110773526-2dd14600-82a0-11eb-9538-a4c66225ced3.png)
 - 더 빨라짐. 이전 frame 중에서 key frame에 해당하는 frame의 feature를 다음 frame에 전달해서 특징 맵의 계산량을 획기적으로 줄임(소형화된 디바이스에 적용 가능)

# Panoptic segmentation
 - 기존의 instance segmentation은 배경에 대한 정보 x
 ![image](https://user-images.githubusercontent.com/43736669/110773889-902a4680-82a0-11eb-9368-3fa06f082104.png)
 - 배경에 관심이 있을 땐 semantic segmentation이 더 좋음
 - 이 두 problem을 다 합친 것

## UPSNet
 ![image](https://user-images.githubusercontent.com/43736669/110774198-e13a3a80-82a0-11eb-8601-d37f1c08feeb.png)
 - FPN 구조 사용(고해상도의 Feature 뽑음)
 - head brunch를 두개로 나눔
  - semantic head : fully conv -> sementic map 뽑음
  - instance head : object detection + mask logics
 - 뒷단에 결과들을 융합하는 panoptic head 추가
 ![image](https://user-images.githubusercontent.com/43736669/110774490-3413f200-82a1-11eb-9375-15cfec235ced.png) 
 - instance mask, 각 물체와 배경에 해당하는 mask가 있음
 - 각 instance들을 bounding box가 아닌 전체 영상에 해당하는 위치에 넣기 위해 semantic head의 물체 부분을 instance에 넣어 최종 물체 위치 표시
 - unknown class를 고려하기 위해 물체의 semantic mask에 instance부분을 제외한 부분(그림의 -부분)을 구해서 unknown 정보로 넣음

## VPSNet
![image](https://user-images.githubusercontent.com/43736669/110775299-1dba6600-82a2-11eb-8b65-949c97bf316b.png)
 - 두 시간차를 가지는 가지는 영상 사이에 파이라는 모션 map을 사용해서 각 frame에서 나온 feature map을 모션에 따라서 warping을 해줌
 - motion map : 한 영상에서 어떠한 포인터가 어디로 이동했는지 대응점들을 모든 픽셀에 대해 모아놓은 map
 - T-t에서 뽑힌 feature이지만 t에서 찍은 것처럼 motion map을 tracking 해줌(옮겨줌), 그리고 원래 각 frame에서 찍혔던 feature을 합쳐서 사용 -> 현재 frame에서 찾지 못한 특징들(가려진 물체 등)을 이전 frame에서 가져옴
 - 시간 연속적으로 smooth한 segmentation이 됨
 - 이후 RoI feature들을 각각 추출해서 기존 RoI들과 현재 RoI들이 어떻게 연관이 되어있는지를 Track Head를 통해 찾아서 연관성을 맞들어 줌
 - 나머지는 ups와 동일(bbox head, mask head, segmantic head)

# Landmark localization
 ![image](https://user-images.githubusercontent.com/43736669/110776583-940b9800-82a3-11eb-9c1a-ce95c1933763.png)
 - 얼굴이나 사람의 몸체 등 중요하다고 생각하는 key point들을 정의하고 추적

## Coordinate regression vs heatmap classification
 - ![image](https://user-images.githubusercontent.com/43736669/110778678-00879680-82a6-11eb-9692-fdd8003dd82d.png)
 - 기존의 box regression처럼 x,y 좌표에 대해 regression 하는 모델을 부정확함(일반화에 문제).
 - heatmap classification : semantic segmentation 처럼 한 채널들이 각각의 keypoint를 담당하게 되고, 각 keypoint마다 하나의 class로 생각해서 keypoint가 발생할 확률들을 각 픽셀별로 classification 하는 방법으로 해결
 
## landmark location to Gaussian heatmap(더 찾아보자...)
![image](https://user-images.githubusercontent.com/43736669/110779120-83a8ec80-82a6-11eb-9fd5-ceb6f0f6bbd0.png)
- 각 위치마다 컨피던스가 나오는 형태. x,y 위치가 label로 주어졌을 때, heatmap label을 생성하는 방법(loc to heatmap)
- x,y 가 gaussian 평균이라고 생각하고, 그 위치에 가우시안을 씌우는 것
- 아래 코드는 x,y가 0,0 라고 생각할 때 가우시안을 씌우는 방법
- 반대로 heatmap에서 loc으로 변환은 어떻게 할까?

## Hourglass Network
 ![image](https://user-images.githubusercontent.com/43736669/110780202-c7502600-82a7-11eb-8ae7-4570be7dd902.png)
 - UNet을 여러 개 쌓은 듯한 구조
  1) 영상 전체를 작게 만들어서 receptive field를 키우기 위해
  2) skip connection이 있어서 low-level feature을 참고
  3) 여러 번 거쳐서 큰 그림과 detail을 합쳐나감
 ![image](https://user-images.githubusercontent.com/43736669/110780257-d931c900-82a7-11eb-9694-23d3e3ca1230.png)
 - UNet과 달리 skip connection이 +연산(dimension 증가가 x)
 - skip connection을 convolution을 통과하여 전달
 
## DensePose 
 ![image](https://user-images.githubusercontent.com/43736669/110780533-23b34580-82a8-11eb-89b1-7c008102c4c3.png)
 - 기존의 sparse 한 모델들과는 다르게 신체 전체를 인식
 - uv map

### uv map
 - 표준 3d model의 각 부위를 2d로 펼쳐서(u,v 축) 이미지 형태로 만들어 놓은 표기법
 ![image](https://user-images.githubusercontent.com/43736669/110780630-3f1e5080-82a8-11eb-9815-d7c7e18de92e.png)
 - uv map의 한 점은 3d mash의 한 점과 1:1 match. 3d mash가 움직여도 map은 보존이 됨(관계가 변하지 않음)
 - uv 좌표를 바로 출력하는 densepose는 3d mash를 바로 출력하는 것과 마찬가지
 - color(texture)를 입히기 위해 고안된 것

### DensePose의 구조
 - Mask R-CNN과 유사
 ![image](https://user-images.githubusercontent.com/43736669/110780990-ab00b900-82a8-11eb-9f9e-203146d2d32d.png)
 - patch : 각 body part의 segmentation map
 - 2d 구조의 cnn으로 3d 구조를 설명

### RetinaFace
 ![image](https://user-images.githubusercontent.com/43736669/110781099-d2f01c80-82a8-11eb-815b-685037b0909a.png)
 - 다양한 Task의 branch를 다 넣어서 multitask 학습
 - backbone network가 더 강하게 학습됨(모든 상황을 고려해서 학습 : 데이터를 더 많이 본 효과) -> 성능향상 폭이 큼
 ![image](https://user-images.githubusercontent.com/43736669/110781368-28c4c480-82a9-11eb-80a9-2291a07a229e.png)
 - backbone network 위에 하고자 하는 task에 해당하는 branch를 넣는 것이 현재 CV의 큰 이슈

# Detecting objects as keypoints
## CornerNet
![image](https://user-images.githubusercontent.com/43736669/110781522-57429f80-82a9-11eb-943f-5167016c7a98.png)
- 두 개의 corner point만 있으면 bounding box가 unique하게 결정
- backbone에서 나온 feature map의 태그를 이용해서 각각의 corner를 검출 -> embedding(각 point가 가지는 정보의 head) -> 학습할 때 같은 box에서 나온 embedding은 같아야 한다는 조건으로 학습
- corner 출력 -> embedding match(corner pair 만들어서) 후 bounding box로 추출
- 성능보다는 속도 강조

## CenterNet
![image](https://user-images.githubusercontent.com/43736669/110781911-cd470680-82a9-11eb-8b89-215ba727de28.png)

- box를 정의하는 Center point 추가(corner + center 학습)

![image](https://user-images.githubusercontent.com/43736669/110781994-ea7bd500-82a9-11eb-83f3-7dec6f9d3e13.png)

- Bounding Box를 정의하는 데 필요한 건 Center point, 폭, 높이
![image](https://user-images.githubusercontent.com/43736669/110782131-1dbe6400-82aa-11eb-8a78-0e9779f4406c.png)

