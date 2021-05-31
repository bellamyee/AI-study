# CNN Based Models
## CHAR
 - Word 단위 classification
    - 이미지를 통째로 넣고 classification
    - 모든 단어에 대한 class를 할당, 어느 class에 속하는지 예측
    - 가장 직관적인 방법
    - OOV(Out of Vocab) 문제가 있음  

![image](https://user-images.githubusercontent.com/43736669/120146652-5d994580-c220-11eb-92db-57c61d38af72.png)
 
 - Character 단위 Classification
     - Word level 말고 character levevl로 classification
     - Max Length(N)를 정해 놓고, CNN에 parallel classifier를 N개 붙여서 왼쪽부터 각 character를 예측하게 함
     - 가변길이를 처리하기 위해 빈 문자(pi)를 추가
     - Max Length를 넘는 단어는 처리가 불가
     - 37 class(a-z + 0-9 + NULL)
 
 ![image](https://user-images.githubusercontent.com/43736669/120146884-bb2d9200-c220-11eb-806f-b3be22585fc4.png)

 - Bags of N-grams classification
    -  Classifier를 1개만 쓰면서 OOV를 없애는 방법
    -  N = 4인 경우, 모든 character들에 대하여 uni-gram, bi-gram, tri-gram, 4-gram을 구하여 class로 할당
    -  Multi-label classification과 같은 형태로 학습

![image](https://user-images.githubusercontent.com/43736669/120147130-29725480-c221-11eb-9a96-55e0351d0704.png)

## CRNN
  - CNN으로 Image의 좋은 Feature를 뽑고
  - 뽑은 feature를 RNN으로 전달해서 Sequence 생성
  - output에서 sequence를 생성하는 방법(-s-taatte -> state)를 CTC라고 함

![image](https://user-images.githubusercontent.com/43736669/120147542-c503c500-c221-11eb-9162-64e3581813fb.png)

  - Height를 최대한 줄여서(32까지) width만 남긴 상태로 RNN에 들어감

![image](https://user-images.githubusercontent.com/43736669/120149952-66404a80-c225-11eb-806a-55c6758ba55d.png)

  - RNN(LSTM Layer로 넣어 Sequence 생성) : 순차적으로 보게 됨(feature map에 대한 output이 순차적으로 사용)

![image](https://user-images.githubusercontent.com/43736669/120150098-9687e900-c225-11eb-842d-7d013dc12e2e.png)

  - Transription Layer에서는 겹치는 부분을 한도막 한도막 보고 최종 sequence를 예측함(CTC algorithm)
  - 음성 인식 분야와 매우 유사

![image](https://user-images.githubusercontent.com/43736669/120150364-eff01800-c225-11eb-8cc1-f96384d34407.png)

### CTC Algorithm

- input과 output 사이의 정확한 alignment를 몰라도 쓸 수 있음(alignment-free algorithm)
- CTC는 input과 output 사이의 모든 가능한 alignment의 가능성을 더하여 계산


![image](https://user-images.githubusercontent.com/43736669/120153100-4874e480-c229-11eb-94c7-176b32c0c498.png)
