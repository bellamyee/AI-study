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
