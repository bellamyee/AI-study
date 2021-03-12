# Multi-modal learning
## Multi-modal learning의 challenge
 1. 데이터 표현의 차이
![image](https://user-images.githubusercontent.com/43736669/110874519-39138880-8317-11eb-8a68-60222c94594d.png)
 2. 정보의 양과 feature space의 특징들이 unbalance(1:N Match)
![image](https://user-images.githubusercontent.com/43736669/110874580-59434780-8317-11eb-8d75-f6dbfc57ecf8.png)
 3. 특정 modality에 치우친 학습이 될 수 있음(대부분의 경우에 쉽게 해결되는 moduality에 치우치게 될 수 있음)
![image](https://user-images.githubusercontent.com/43736669/110874636-7415bc00-8317-11eb-9aaf-8302457ea27d.png)

## Multi-modal learning의 학습 패턴
![image](https://user-images.githubusercontent.com/43736669/110874829-cd7deb00-8317-11eb-821b-0083a6760e51.png)
두 modal을 같은 공간에서 매칭시키거나, 하나의 modal을 다른 modal로 translation, 하나의 modal에서 같은 modal로의 출력을 위해 다른 modal을 활용

# Multi-modal tasks
## Visual & Text data
### joint embedding
 - Matching을 하기 위한 task
#### image tagging
![image](https://user-images.githubusercontent.com/43736669/110876426-d02e0f80-831a-11eb-8618-e267ddcd369a.png)
tag to image / image to tag task

##### 구현 방법

![image](https://user-images.githubusercontent.com/43736669/110876481-e2a84900-831a-11eb-9f30-fb615620a6da.png)
 - pre-trained model을 합쳐서 학습시키는 방법
 - 두개의 dimension을 같게 만들어서 호환성이 있도록 joint embedding 학습


![image](https://user-images.githubusercontent.com/43736669/110876599-2c912f00-831b-11eb-9423-9109186d67f3.png)
 - Text와 Image를 같은 공간에 embedding 하고, 서로 연관성이 있을 시 가까운 거리(push), 없을 경우 먼 거리가 되도록(pull) 학습 : distance 기반의 metric learning

![image](https://user-images.githubusercontent.com/43736669/110876734-737f2480-831b-11eb-84c9-cc4d33f4c589.png)
 - 덧셈 뺄셈 등 벡터와 유사한 특징들을 띄게 됨

![image](https://user-images.githubusercontent.com/43736669/110876882-bb05b080-831b-11eb-88d0-8cac7417ca17.png)
 - food image를 보고 recipe를 출력하는 모델을 생각해 보자
 - 재료들이 어떤 순서로 추가가 될 지를 rnn 계열의 network를 통해 하나의 fixed dimension vector로 만들어 줌-> text를 대표하는 embedding 만듬
 - image 또한 하나의 embedding으로 만듬
 - 서로 연관이 되었다면 cosine siliarity loss 높게 아니라면 낮게
 - high-level을 위해 다른 semantic regulrization 추가

#### Cross modal translation
##### image captioning
- image를 잘 설명하는 text description을 생성하는 모델
![image](https://user-images.githubusercontent.com/43736669/110877119-3bc4ac80-831c-11eb-80ea-41c624c3a372.png)
- image를 input으로 다루기 위해 cnn, sentence를 출력하기 위해 rnn 사용
![image](https://user-images.githubusercontent.com/43736669/110877187-5dbe2f00-831c-11eb-82ec-eb3aab52f397.png)
- image의 cnn output이 rnn의 시작 토큰이 됨
![image](https://user-images.githubusercontent.com/43736669/110877354-9fe77080-831c-11eb-8186-f8dbbb7df8c1.png)
- show, attend, tell : 각 출력해야 할 단어에 따라 어느 부분에 attention을 둘 지가 다름
- input image를 14x14 의 공간 정보를 가지고 있는 feature map들로 만듬
- RNN에서 해당 feature map들을 각각 참고하여 단어들을 만듬
![image](https://user-images.githubusercontent.com/43736669/110877629-053b6180-831d-11eb-857d-8fd439c0b494.png)
- 사람의 attention과 유사하게 feature가 들어오면 어디를 attention 해야할지 heatmap으로 만들고 해당 heatmap과 feature을 결합해서 z를 만듬

###### 모델 작동 순서
![image](https://user-images.githubusercontent.com/43736669/110877778-4cc1ed80-831d-11eb-9195-603d2f68d2a9.png)
 - image에서 CNN을 이용해 feature map을 얻어 LSTM의 condition으로 넣음
![image](https://user-images.githubusercontent.com/43736669/110877821-67946200-831d-11eb-9598-dbc9a1205740.png)
 - 거기서부터 어떤 부분을 attention 할지 출력
 - 해당 weight를 feature와 combination을 해 z1을 생성
![image](https://user-images.githubusercontent.com/43736669/110877972-af1aee00-831d-11eb-822d-e9855f1ffb2a.png)
 - RNN condition에 z1과 start word token을 넣어줌
![image](https://user-images.githubusercontent.com/43736669/110878032-d2de3400-831d-11eb-869d-1bafde6c57a4.png)
 - 시작 단어를 유추
 - 다음엔 어디를 ref 할지를 예측(좌측 attention map)
![image](https://user-images.githubusercontent.com/43736669/110878147-fdc88800-831d-11eb-897e-2564c8ab6feb.png)
 - 해당 attention(갈매기)을 feature와 inner product해서 z2를 생성
 - y2로는 이전 출력 단어 넣음
![image](https://user-images.githubusercontent.com/43736669/110878211-1c2e8380-831e-11eb-83fa-10b9e2da0b8b.png)
 - 다음 단어 출력
 - s3(다음 attention)을 

##### Text to image generative model
 ![image](https://user-images.githubusercontent.com/43736669/110878283-4da74f00-831e-11eb-9e9f-7e3e8541bf39.png)
 - one to many model이므로 generative model을 모델링
 
 ![image](https://user-images.githubusercontent.com/43736669/110878329-5e57c500-831e-11eb-8085-cd38ad63619b.png)
 conditional GAN
 - generator : text 전체를 fixed dimension으로 만들고, Gaussian random code를 추가해 diverse 한 output이 나올 수 있도록 하고 decoder를 거쳐 image generate
 - discriminator : image를 input으로 받아 encoder를 거쳐 low-dimension spatial feature 뽑음 -> sentence 정보를 같이 받음 -> sentence condition 하에 입력된 영상이 make sense or not 판단하도록 학습

#### cross modal reasoning
##### Reasoning task : visual question answering
 - 영상과 질문으로부터 답을 유추
![image](https://user-images.githubusercontent.com/43736669/110878649-edfd7380-831e-11eb-94c5-45f3905ec0e7.png)
 - Image encoder : pre-trained nn을 통해 fixed dimension 출력
 - Question encoder : rnn계열 통해 fixed dimension 출력
 - point-wise multiplication : 두 개의 embedding feature가 서로 interaction 할 수 있도록 만듬

### Visual data & Audio task
#### Sound data representation
![image](https://user-images.githubusercontent.com/43736669/110879114-c22ebd80-831f-11eb-934f-798b99356283.png)
 - 1d sound를 spectogram이나 MFCC 형태의 Acoustic feature로 변환 
![image](https://user-images.githubusercontent.com/43736669/110879230-ebe7e480-831f-11eb-97c6-72ae243d7c5d.png)
 - 변환 방법
 - fourier transform : 시간축의 waveform을 주파수 축으로 바꿔주는 것
 - 굉장히 짧은 window 구간 동안 Fourier transform을 사용하는 것
