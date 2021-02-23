# 경사 하강법
## 미분과 경사 하강법
 - 미분을 통해 접선의 기울기를 구하고, 한 점에서 접선의 기울기를 알면 어느 방향으로 점을 움직여야 함수값이 증가/감소하는지 알 수 있다.
 
 - 미분값을 더하면 경사 상승법(극대값 위치), 미분값을 빼면 경사 하강법(극소값 위치)
 
 ![image](https://user-images.githubusercontent.com/43736669/108784551-fdf12580-75b2-11eb-835d-20183e57071d.png)
 
 ![image](https://user-images.githubusercontent.com/43736669/108784582-119c8c00-75b3-11eb-944d-c8b774cd3ff6.png)
 
 - 또한 경사상승/경사하강 방법은 극값에 도달하면 움직임을 멈춘다.
 
 - 실제 알고리즘의 경우 gradient의 크기가 설정한 epsilon 값보다 작아질 때 까지 학습을 실시한다.
 
 ![image](https://user-images.githubusercontent.com/43736669/108785073-0c8c0c80-75b4-11eb-848f-ef955e9bbf20.png)

 
## 벡터 변수에 대한 경사 하강법
 - 벡터가 입력인 다변수 함수의 경우 편미분을 이용한다.
 
 ![image](https://user-images.githubusercontent.com/43736669/108784774-70620580-75b3-11eb-8447-37301ee5b5fc.png)
 
 - 각 변수 별로 편미분을 계산한 gradient 벡터를 이용하여 경사하강/경사상승에 사용한다.
 
 ![image](https://user-images.githubusercontent.com/43736669/108784852-9ab3c300-75b3-11eb-98e8-9e6dbb1a22ca.png)
 
 - 이 경우 각 점에서 가장 빨리 감소하게 되는 방향으로 gradient 벡터가 생성된다.
 
 - 알고리즘의 경우 gradient의 norm이 epsilon 값보다 작아질 때 까지 학습을 실시한다.
 
 ![image](https://user-images.githubusercontent.com/43736669/108785205-4826d680-75b4-11eb-84b0-93cc20f22547.png)

## 경사하강법과 선형 회귀
 
 - 선형 회귀의 목적식은 ||y-Xb|| 이고 이를 최소화하는 b를 찾아야 하므로 다음과 같은 gradient 벡터를 구해야 함
 
 ![image](https://user-images.githubusercontent.com/43736669/108786958-1a439100-75b8-11eb-82ef-e2df64225e6f.png)

 ![image](https://user-images.githubusercontent.com/43736669/108787073-5676f180-75b8-11eb-95ed-46771a2803bc.png)

## Stochastic Gradient Descent

 - 기존 경사하강법은 미분가능하고 볼록(convex)한 함수에 대해선 적절한 학습률과 학습횟수를 선택했을 때 수렴이 보장되어 있음(특히 선형 회귀)

 - but 비선형회귀 문제의 경우 목적식이 볼록하지 않을 수 있으므로 수렴이 항상 보장되지는 않음
 
 - stochastic gradient descent는 모든 데이터를 사용해서 업데이트하는 대신 데이터를 일부만 사용하여 업데이트함.

 - 
