# Detection & Segmentation
## Model History
![image](https://user-images.githubusercontent.com/43736669/116013095-46879680-a669-11eb-9991-30281e3bfc58.png)  
 - Shervin Minaee, Yuri Boykov, ‘Image Segmentation Using Deep Learning: A Survey”
### Detection Model History
![image](https://user-images.githubusercontent.com/43736669/116013163-a0885c00-a669-11eb-9a03-6d160432efa8.png)
#### Fast, Faster R-CNN
 - 객체가 있을 후보 영역을 제시한 후 해당 영역에 객체가 있을 지 등을 예측. 객체 후보 영역 예측과 객체의 예측 2단계로 이루어짐. -> 이후 해당 단계로 인한 문제점들 해결할 수 있는 모델들로 발전

## COCO Format
- info : dataset에 대한 high-level 정보 포함  
![image](https://user-images.githubusercontent.com/43736669/116037670-650a8380-a6a3-11eb-8c38-c6a7ba7167ea.png)
- licenses : image의 license 목록  
![image](https://user-images.githubusercontent.com/43736669/116037724-73f13600-a6a3-11eb-876b-e71034c0991d.png)
- images : dataset의 전체 image목록 및 각각의 width, height,파일명 등 포함  
![image](https://user-images.githubusercontent.com/43736669/116037801-8d927d80-a6a3-11eb-8d4b-700ac7d04e48.png)
- categories : class id, name, supercategory 포함  
![image](https://user-images.githubusercontent.com/43736669/116037855-a26f1100-a6a3-11eb-9ac3-08a87f532c3e.png)
- annotations : image의 자세한 라벨 정보  
![image](https://user-images.githubusercontent.com/43736669/116037911-b581e100-a6a3-11eb-81d3-39742a13182b.png)
- segmentation : 각 class에 대한 pixel의 x,y좌표  
![image](https://user-images.githubusercontent.com/43736669/116037983-cfbbbf00-a6a3-11eb-9852-edadddeb6415.png)
- bbox : 좌상단 (x,y), width, height  
![image](https://user-images.githubusercontent.com/43736669/116038079-ecf08d80-a6a3-11eb-9e8b-1c3ae108798b.png)
