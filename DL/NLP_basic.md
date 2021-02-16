# Natural Language Processing
## Academic Disciplines
 - Major conferences : ACL, EMNLP, NAACL 
### low - level parsing

## Word Embedding
### Word Embedding 이란?
 - 단어를 벡터로 표시하는 것 
 - 유사한 단어는 좌표공간 상 가까운 거리, 유사하지 않은 단어는 먼 거리 
 
## Bag of words represntation

 - Step 1. unique words 의 단어장을 구성
   - "John really really loves this movie" => {"John", "really", "loves", "this", "movie" }
 
 - Step 2. one-hot 벡터로 만들어줌
   - John : [1 0 0 0 0 0 0], really : [0 1 1 1 1 1 1 1] ...  
   - 모든 단어의 거리는 sqrt(2), cosine similarty는 0 
   -> Sentence가 one hot의 합 벡터로 나타내짐. ex) [1 2 1 1 1 0 0 0]
  
 ### 베이지안 rule
 ![image](https://user-images.githubusercontent.com/43736669/108024679-5fbc0780-7068-11eb-9cb8-fa4682ff2df6.png)
 ![image](https://user-images.githubusercontent.com/43736669/108025344-a827f500-7069-11eb-9015-c00e41595c9c.png)
 ![image](https://user-images.githubusercontent.com/43736669/108028280-effd4b00-706e-11eb-98a8-cc67aa89d594.png)
 ![image](https://user-images.githubusercontent.com/43736669/108029091-3acb9280-7070-11eb-9379-2713c4ace983.png)
 ![image](https://user-images.githubusercontent.com/43736669/108029123-47e88180-7070-11eb-8b95-e266cbb03b7a.png)

## Word2Vec
 - 단어를 벡터로 표현하기 위한 알고리즘 
 - 유사한 context의 단어는 유사한 의미를 가진다고 가정 
 ![image](https://user-images.githubusercontent.com/43736669/108029485-d957f380-7070-11eb-9de8-a8002b99384f.png)
