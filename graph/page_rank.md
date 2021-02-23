# Page Rank Algorithm

## 웹과 그래프
 - 웹은 웹페이지와 하이퍼링크로 구성된 거대한 방향성 있는 그래프.
 - 각 웹 페이지가 정점, 하이퍼링크는 나가는 간선.
 - 추가적으로 키워드 정보를 포함하고 있음 
 ![image](https://user-images.githubusercontent.com/43736669/108789290-4ca3bd00-75bd-11eb-99c4-a167b6b68cba.png) 

## 구글 이전의 검색 엔진(기존의 검색 방법)
 - 웹페이지를 거대한 디렉토리로 정리하는 방식 -> 카테고리의 수가 무한정 커짐. 카테고리 구분이 모호함 
 - 키워드에 의존한 검색 엔진 -> 사용자가 검색한 키워드를 여러 번 포함한 페이지를 반환 -> 악의적인 웹 페이지에 취약

## 페이지 랭크 알고리즘
 ### 투표
  - 페이지랭크 핵심 아이디어는 투표(하이퍼링크)
  - 투표(하이퍼링크)를 통해 사용자 키워드와 관련성이 높고 신뢰할 수 있는 웹페이지를 찾음
  - 웹페이지 u가 v로의 하이퍼링크를 포함한다면, u의 작성자가 판단하기에 v가 관련성이 높고 신뢰할 수 있다.
  - 즉, u가 v에게 투표했다!
  - -> 들어오는 간선 수가 많을 수록 신뢰할 수 있다.
  - 악용될 소지가 있음. 웹페이지를 여러 개 만들어서 간선의 수를 부풀릴 수 있음.
 
 ### 악용 방지법
  - 가중 투표 : 관련성이 높고 신뢰할 수 있는 웹사이트의 투표를 더 중요하게 간주
  - but, 관련성과 신뢰성은 알고리즘의 output일텐데 어떻게 측정하지? 재귀, 연립방정식 풀이

 ### 페이지 랭크 알고리즘 : 투표 관점
  - 측정하려는 웹페이지의 관련성 및 신뢰도를 페이지랭크 점수라고 한다면,
  ![image](https://user-images.githubusercontent.com/43736669/108789815-7dd0bd00-75be-11eb-979c-b0bdfbfb081a.png)
  ![image](https://user-images.githubusercontent.com/43736669/108789911-bbcde100-75be-11eb-8edd-0c4aa440254c.png)
  ![image](https://user-images.githubusercontent.com/43736669/108789937-d0aa7480-75be-11eb-8d23-0cce13b25ebf.png)
  
### 페이지 랭크 알고리즘 : 임의 보행 관점
  - 페이지랭크는 Random Walk의 관점에서도 정의할 수 있음
  - 랜덤하게 웹을 서핑하는 웹 서퍼를 가정 : 현재 웹페이지에 있는 하이퍼링크 중 하나를 균일한 확률로 클릭
  ![image](https://user-images.githubusercontent.com/43736669/108790170-62b27d00-75bf-11eb-8ad8-f39653d5939a.png)
  - (j로 갈 수 있는 모든 i에 대해, t번째에 i에 있을 확률 / 해당 i의 나가는 간선 수) 
  - 웹 서퍼가 이 과정을 무한히 반복하면(t가 무한히 커지면), 확률분포 p(t) 는 수렴. 즉 p(t) = p(t+1) = p
  ![image](https://user-images.githubusercontent.com/43736669/108791146-bc1bab80-75c1-11eb-96e3-4283bc6b25cc.png)
  ![image](https://user-images.githubusercontent.com/43736669/108791177-d2296c00-75c1-11eb-9c63-0eb17310bffe.png)

## 페이지랭크의 계산
### 페이지랭크의 계산 : 반복곱
 - 페이지랭크 점수의 계산에는 반복곱(power iteration)을 사용
 ![image](https://user-images.githubusercontent.com/43736669/108791392-4e23b400-75c2-11eb-860e-2f3e9d728ea9.png)
 - 수렴 : r(t) = r(t+1) + eps => 이때의 r(t) 값을 페이지랭크의 값으로 반환
 ![image](https://user-images.githubusercontent.com/43736669/108791631-e28e1680-75c2-11eb-9d23-f05326b517de.png)
 
### 문제점과 해결책
#### 반복곱이 항상 수렴하는 것을 보장할 수 있나요?
![image](https://user-images.githubusercontent.com/43736669/108791777-3e589f80-75c3-11eb-8a9b-0e37e496fd87.png)

#### 반복곱이 합리적인 점수로 수렴하는 것을 보장할 수 있나요?
![image](https://user-images.githubusercontent.com/43736669/108791808-4ca6bb80-75c3-11eb-970b-f2e28831a0f2.png)

#### 해결책
 - 순간이동(Teleport) 도입
  - 현재 페이지에 하이퍼링크가 없다면, 임의의 웹페이지로 순간이동
  - 현재 웹페이지에 하이퍼링크가 있다면, a의 확률로 하이퍼링크 중 하나 클릭 or 1-a의 확률로 임의의 웹페이지 순간이동
  - a = Damping Factor
 ![image](https://user-images.githubusercontent.com/43736669/108802954-c5664180-75dc-11eb-8d85-9bfa953cb901.png)
 
