# FCN의 한계점
1. 객체의 크기가 크거나 작은 경우 예측을 못함
2. Object의 디테일한 모습이 사라짐(Deconv 절차가 너무 간단)

# DeconvNet  
## Architecture  
![image](https://user-images.githubusercontent.com/43736669/116566342-a28c3c80-a941-11eb-95f1-e6f3867e9e14.png)
- Decoder를 Encoder와 대칭으로 만든 형태
- Conv Network는 VGG16을 사용
- 13개의 층으로 이루어짐
- ReLU와 Pooling이 Convolution 사이에서 이루어짐

![image](https://user-images.githubusercontent.com/43736669/116566391-b20b8580-a941-11eb-9d6c-bc537f0dec04.png)  
- 뒷부분은 Unpooling과 Transposed Convolution이 반복적으로 이루어짐

## Unpooling  
![image](https://user-images.githubusercontent.com/43736669/116566637-e121f700-a941-11eb-8e91-d193c55fc05c.png)  
- Pooling 시 max index를 저장해 그 부분을 복원
- 학습 필요 x 속도 빠름
- sparse matrix를 가지게 되므로 값을 채워야 하는데 이를 trasposed convolution으로 해결

## Deconvolution(Transposed Convolution)  
![image](https://user-images.githubusercontent.com/43736669/116566911-1dedee00-a942-11eb-87ef-68d338fbfe72.png)  
- Sparse map -> Dense
- 순차적인 층의 구조로 얕은층의 경우 전반적인 모습, 깊은 층의 경우 구체적인 모습을 잡아냄

## DeconvNet의 계층별 특징
![image](https://user-images.githubusercontent.com/43736669/116567251-6c02f180-a942-11eb-8501-3a2f9a14af75.png)
- Unpooling의 경우, example-specific한 구조를 잡아냄(자세한 구조)
- Transposed Conv의 경우 class-specific한 구조를 잡아냄(위의 구조에 빈 부분을 채움)

## DeconvNet vs SegNet  
![image](https://user-images.githubusercontent.com/43736669/116570559-517e4780-a945-11eb-9741-41bf1c4f7b66.png)

# FC DenseNet
## Skip Connections
![image](https://user-images.githubusercontent.com/43736669/116570979-a28e3b80-a945-11eb-9c5b-5b8a714a8a20.png)

## Architecture
![image](https://user-images.githubusercontent.com/43736669/116571455-0e70a400-a946-11eb-9c3e-d47f6be9ba9a.png)
