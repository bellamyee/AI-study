# 파이프라인의 빠른 반복
## 고성능 장비 필요, 1~2달간 하루 평균 4시간, 주말 평균 8시간 투자
# 점수 개선 아이디어
## Notebooks 탭 참고, Discussion 탭 참고
# 검증 전략
## strafied k-fold : 거의 항상 사용
![image](https://user-images.githubusercontent.com/43736669/109921714-a6b02b00-7cff-11eb-9b09-5074975aa3f9.png)
# 앙상블
![image](https://user-images.githubusercontent.com/43736669/109921781-bc255500-7cff-11eb-9d9a-64f2aa38fd0e.png)
## 주피터에서 터미널 열면 크롬창 닫아도 살아있음

## pretrained 모델이 있는 최신 기술 쓰면 성능 좋아짐
## 오픈소스 보고 따라치기
## 은메달 까지의 팁 : 앙상블, 학습데이터, unlabel된 데이터를 내 모델로 가짜 레이블을 붙여서 다시 학습에 사용
## lr = 0.001, 스케쥴러 = multistep-lr
## 공부할 땐 팀수가 많은 대회
## 배치사이즈 메모리 용량이 허용하는 한 최대한 크게(전체 데이터 사이즈의 10%보다는 적지만 그이하에선 메모리 최대치로)
