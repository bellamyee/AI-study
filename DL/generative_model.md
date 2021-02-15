# Generative Model
## Generative Model 이란?
- implicit model(generation) + explicit model(discrimination)

## Basic Discrete Distributions(일반적)

### Bernoulli distribution : coin flip
 - 숫자가 하나 필요함
 
### Categorical distirbution : m-sided dice
 - 숫자가 m-1개 필요함

## Example
### n개의 픽셀화된 바이너리 이미지가 존재한다고 했을 때, 
 - 가능한 state 수 : 2^n
 - 필요한 parameter 수 : 2^n - 1 

### 픽셀끼리 independent라고 가정한다면, P(x1,...,xn) = P(X1)P(X2)...P(Xn)

 - 가능 state 수 : 2^n
 - 필요한 parameter 수 : n
 
 따라서 independence assumption이 매우 중요하고 강력하다!
 
### -> Conditional Independence 라는 Trick을 사용
![image](https://user-images.githubusercontent.com/43736669/107911585-3cc62080-6fa0-11eb-8580-fdf1fdb2cbb9.png)

![image](https://user-images.githubusercontent.com/43736669/107911778-8b73ba80-6fa0-11eb-94ca-667f7c74c41e.png)
### 지금은 앞선 dependent 가정과 동일하므로 똑같은 수의 parameter가 필요하다
![image](https://user-images.githubusercontent.com/43736669/107912032-11900100-6fa1-11eb-9d52-25069846d309.png)
### 위와 같이 markov assumtion을 사용하면(바로 전 확률에만 dependent) exponential reduction을 유도 할 수 있다! (= auto regressive model)

# Auto regressive model 
