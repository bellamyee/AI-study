# RNN Basic

## SEQUENCE DATA

### sequence data란?
- 소리, 문자열, 주가 등의 데이터.

- 독립동등분포 가정을 잘 위배하기 때문에 과거 정보의 손실을 줄여야 함

### sequence 데이터 다루기

- 이전 시퀀스의 정보를 가지고 앞으로 발생할 데이터의 확률분포를 다루기 위해 조건부확률 이용<br>

![image](https://user-images.githubusercontent.com/43736669/106897086-cc183c00-6735-11eb-9df0-fecf1df82d04.png)<br>
- 따라서 시퀀스 데이터를 다루기 위해선 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요

## RNN

### RNN의 이해

 - 가장 기본적인 RNN 모형은 MLP와 유사한 모양

![image](https://user-images.githubusercontent.com/43736669/106900903-6ed2b980-673a-11eb-839e-54d0d9b02d29.png)
