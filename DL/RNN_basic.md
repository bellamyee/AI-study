# RNN Basic

## SEQUENCE DATA

### sequence data란?
- 소리, 문자열, 주가 등의 데이터.

- 독립동등분포 가정을 잘 위배하기 때문에 과거 정보의 손실을 줄여야 함

### sequence 데이터 다루기

- 이전 시퀀스의 정보를 가지고 앞으로 발생할 데이터의 확률분포를 다루기 위해 조건부확률 이용<br>

![image](https://user-images.githubusercontent.com/43736669/106897086-cc183c00-6735-11eb-9df0-fecf1df82d04.png)<br>
- 따라서 시퀀스 데이터를 다루기 위해선 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요(기존의 모델 사용 불가)

## SEQUENCE MODEL

### Naive sequence model

 ![image](https://user-images.githubusercontent.com/43736669/106905889-f8d15100-673f-11eb-975e-aee42ddacb64.png)
 
 - 과거의 고려해야 할 정보량이 점점 늘어남 -> 고려할 시간 량을 고정한다면 해결
 
### Markov model(first-order autoregressive model)
 
 - 가정 : 나의 현재는 바로 직전 과거에만 DEPENDENT 하다!
 
 ![image](https://user-images.githubusercontent.com/43736669/106907746-ef48e880-6741-11eb-8efc-3f4af2960088.png)
  
 - 장점 : joint distribution을 표현할 때 굉장히 편함
 
 - 단점 : 과거의 많은 정보를 고려해야하는데, 그러질 못함
 
### Latent autoregressive model

 ![image](https://user-images.githubusercontent.com/43736669/106908068-48188100-6742-11eb-8387-1b5c267bd907.png)
 
 - 앞선 모델들의 단점(과거의 정보 고려)을 극복.
 
 - 과거의 정보들을 Hidden state 하나에 summarize하여 저장하고, 거기서만 정보를 가져옴
 

## RNN

### RNN의 이해
 - 
 - 가장 기본적인 RNN 모형은 MLP와 유사한 모양(자기 자신으로 돌아오는 구조가 추가)<br>
 
 ![image](https://user-images.githubusercontent.com/43736669/106908817-00dec000-6743-11eb-8656-2c3bd54552a2.png)

 - 현재의 입력과 과거의 입력이 Recurrent 하게 들어옴
 
 ![image](https://user-images.githubusercontent.com/43736669/106909702-e2c58f80-6743-11eb-9193-6a5de3da0c82.png)

 - 이를 시간순으로 풀게 되면, 결국 Fully connected(shared weight) 
 
 - RNN은 이전 순서의 잠재변수와 현재의 입력을 활용하여 모델링

![image](https://user-images.githubusercontent.com/43736669/106900903-6ed2b980-673a-11eb-839e-54d0d9b02d29.png)

![image](https://user-images.githubusercontent.com/43736669/106902336-0e447c00-673c-11eb-9046-053c49c45995.png)
 
 - forward propagation 은 이렇게 
 
 ![image](https://user-images.githubusercontent.com/43736669/110049446-2cca8100-7d95-11eb-84f2-9915fb176ce7.png)

 <br>
 
 - 역전파는 잠재변수의 연결 그래프에 따라 순차적으로 계산(BPTT)
 
 ![image](https://user-images.githubusercontent.com/43736669/106903768-c0307800-673d-11eb-8a6c-1af27fd4511d.png)

 - 위와 같이 sequence 값이 커질 수록, 미분값이 엄청 커지거나, 엄청 작아지거나.<br>
 - gradient가 0으로 줄어드는게 큰 문제가 되므로 길이를 끊는 것이 필요(=truncated BPTT)<br>
 - 또한, 과거의 정보가 사라질 확률이 높음 = long term dependency를 잡는게 되게 어렵다
 
 - 위와 같이 굉장히 많은 W를 계속 곱하는 형태가 됨 
 
 ![image](https://user-images.githubusercontent.com/43736669/106966657-1b3b8c80-6789-11eb-995a-58971e724994.png)

 - activation function이 sigmoid라면 vanishing gradient, RELU라면 exploding gradient 현상 발생  
 
 - 이런 문제들 때문에 등장한 모델이 LSTM, GRU
 
## LSTM
