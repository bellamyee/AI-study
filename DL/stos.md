# Sequence to sequence model

## Sequence to sequence model 이란?
 - RNN 중 Many to Many type(입력 : word 단위 문장, 출력 : word 단위 문장) 
 ![image](https://user-images.githubusercontent.com/43736669/108313172-37b0dd80-71fb-11eb-9f3f-5bad36dcecde.png) 
 - 입력 문장을 encoder, 출력 문장을 decoder
 - 내부는 lstm

## Sequence to sequence model Attention
 - 위 s to s 모델은 lstm이 long term dependency를 해결했다고 하더라도, 앞쪽에 나온 단어를 잘 번역하지 못하는 문제가 있음 
 - 특히 주어의 소실이 문제가 됨. 이 경우에 이전엔 문장을 역순으로 바꾸는 trick 을 사용.
 
 ### Attention 개념 
 - decoder에서는 encoder의 마지막 hidden state vector만을 사용하는 것이 아니라, 그때그때 필요한 hidden state를 가져와서 사용 
 ![image](https://user-images.githubusercontent.com/43736669/108314116-b78b7780-71fc-11eb-90ef-04907d42b245.png)

 ### Attention 의 작동과정
 - ![image](https://user-images.githubusercontent.com/43736669/108317939-64b4be80-7202-11eb-914a-1f1ab127542e.png)
