# OCR
## OCR(STR) 이란?
 - OCR : Optical Character Recognition 
 - STR : Scene Text Recognition (생활속 이미지 글씨, 다양한 배경, 글씨체 형태 등)  

![image](https://user-images.githubusercontent.com/43736669/119298839-c587e300-bc98-11eb-8adf-20b1f1995db9.png)  

## OCR Task Overall
- 글자의 위치를 찾고 -> 글자를 읽는다

![image](https://user-images.githubusercontent.com/43736669/119298911-ef410a00-bc98-11eb-836b-0da48bd77715.png)

## OCR ALgorithms

### 글자의 위치를 찾는 방법(Text Localization)
  - Object Detection 활용
  - Instance Segmentation 활용
  - Hybrid : Detection, Segmentation 모두 활용

![image](https://user-images.githubusercontent.com/43736669/119299279-93c34c00-bc99-11eb-8636-c98ff5369f86.png)

### 글자를 인식하는 방법(Text Recognition)
  - CNN을 활용하여 Image의 Feature를 뽑음
  - 인식
    - 전체 단어를 한번에 인식
    - Character의 Sequence로 인식
  - 영상처리 및 자연어 처리 알고리즘 모두 사용 가능

# Object Detection
## Overall Architecture
![image](https://user-images.githubusercontent.com/43736669/119683355-8adf9f80-be7e-11eb-9917-b9dadebb984c.png)  
- backbone은 일반적 CNN 형태
- backbone의 feature를 거꾸로 보내 size를 점점 키우는 형태로 Neck을 만들고, 앞의 Feature들과 합쳐 결과를 만듬
- One Stage : Dense Prediction에서 끝남
- Two Stage : 뽑아진 bounding box를 한번 더 들고가서 추가로 작업

## Faster R-CNN  
### Overall Architecture  
![image](https://user-images.githubusercontent.com/43736669/119683870-ff1a4300-be7e-11eb-88c7-1e2c5a8720f5.png)  
- Two Stage 계열 알고리즘
- Input Image가 Convolution Net을 통과하여 Feature(3dim)를 뽑아냄
- RPN이 Bounding Box의 Proposal을 뽑아줌
- 뽑혀진 bounding box를 RoI pooling해서 classify

### Region Proposal Network
![image](https://user-images.githubusercontent.com/43736669/119684200-47396580-be7f-11eb-8925-f350a804f9aa.png)
- Image Feature에서 무언가를 더 하는건데 사실상 이 부분도 Conv Net임
- 앞의 Dense Prediction과 같은 형태로 뽑아냄
