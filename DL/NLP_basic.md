# 1. Academic Disciplines

## 1.1) NLP
### Major conferences : ACL, EMNLP, NAACL 

### low - level parsing 
 - tokenization, stemming(어미의 변화 등) 
 - 각 단어를 위한 의미 단위의 가장 low level

### word and phrase level 
 - Named entity recognition(NER) : 여러 단어로 이루어진 고유 명사 인식(ex.New York Times)
 - part-of-speech(POS) tagging : word들이 문장에서 성분이 무엇인지(S, V, O, ...) 인식하는 tas

### Sentence level
 - Sentiment analysis : 감성 분석
 - machine translation : 번역

### Multi-sentence and paragraph level
 - Entailment prediction : 각 문장간의 논리적 관계 유추
 - Question answering
 - Dialog systems : 챗봇 등 대화
 - Document summarization

## 1.2) Text mining 
ex1) 과거 1년동안 나온 뉴스의 키워드를 모아서 키워드 빈도수 분석하여 특정 연예인의 이미지가 어떻게 변하는지 등 trend 분석 
ex2) 상품에 대한 소비자 반응 키워드 분석(Groupping)


### major conferences : KDD, The Webconf(fomerly,wWWW), WSDM, CIKM, ICWSM)

## 1.3) Information retrieval
### major conference : SIGIR, WSDM, CIKM, RecSys)

- 소셜 사이언스와 고도로 연관됨 
- 검색, 추천시스템 등 

# 2. Trends of NLP
 - 모든 단어들이 하나의 벡터로 표현됨(Word2Vec, GloVe 등을 이용) : word embedding
 - RNN 계열 모델(LSTM, GRU 등) 이 NLP task의 main architecture가 됨
 - RNN 기반의 자연어 처리 모델을 완전히 대체할 수 있는 transformer model이 등장. self-attention을 사용하며 현재 대부분의 자연어 처리 모델은 transformer 모델 기반
 - transformer 모델은 원래 machine translation을 위해 등장.
 - transformer는 영상처리, 시계열 예측, 신약 개발 등 다양한 분야에도 활발히 적용
 - transformer 이전에는 NLP task에 각각 특화된 모델이 적용되어 왔으나, transformer가 도입되며 self-attention 모듈을 stack한 모델들이 그 자리를 대체(BERT, GPT-3, ...)
 - 각 task에 trasnfer learning을 적용한 형태가 각각 특화된 모델보다 월등하게 나은 성능을 보여줌

# Bag-of-Words

## Bag-of-Words representation
1) 단어장을 만들기 : "John really really loves this movie", "Jane really likes this song" -> {"John","really","loves","this","movie","Jane","likes","song"} 
2) 각각의 word를 categorical variable, 즉 one hot으로 표현 John : [1 0 0 0 0 0 0 0], ... , Jane : [0 0 0 0 0 1 0 0 ], ... -> 모든 단어의 거리는 root2, cosine sim은 0
3) 문장은 one-hot 벡터의 합으로 표현됨. "John really really loves this movie" -> John + really + really + loves + this + movie : [1 2 1 1 1 0 0 0]
4) classifier로 분류
  
### 베이지안 rule
 ![image](https://user-images.githubusercontent.com/43736669/108024679-5fbc0780-7068-11eb-9cb8-fa4682ff2df6.png)
 ![image](https://user-images.githubusercontent.com/43736669/108025344-a827f500-7069-11eb-9015-c00e41595c9c.png)
 ![image](https://user-images.githubusercontent.com/43736669/108028280-effd4b00-706e-11eb-98a8-cc67aa89d594.png)
 ![image](https://user-images.githubusercontent.com/43736669/108029091-3acb9280-7070-11eb-9379-2713c4ace983.png)
 ![image](https://user-images.githubusercontent.com/43736669/108029123-47e88180-7070-11eb-8b95-e266cbb03b7a.png)

# Word Embedding
## Word Embedding 이란?
 - Word를 vector로 표현하는 것
 - 유사한 단어는 유사한 vector representations를 가지는 것
 - 유사하지 않은 단어는 far distance를 가지는 것


## Word2Vec
 - 단어를 벡터로 표현하기 위한 알고리즘  
 - 유사한 context의 단어는 유사한 의미를 가진다고 가정 
 - 문장에서 인접한 단어는 유사하다고 가정
 ![image](https://user-images.githubusercontent.com/43736669/108029485-d957f380-7070-11eb-9de8-a8002b99384f.png)
 - cat과 인접한 단어에서 각 단어가 나올 확률분포를 학습
 ![image](https://user-images.githubusercontent.com/43736669/109976840-8d2ed380-7d3f-11eb-932b-4c695e168e48.png)

### Word2Vec 알고리즘의 작동 방식(복습하기!!!!!!!!!!!)
![image](https://user-images.githubusercontent.com/43736669/109977723-776dde00-7d40-11eb-910a-1ce24e389d07.png)
 1) Sentence로부터 Vocabulary 추출
 2) Voc를 Voc 크기만큼의 dim을 가지는 one-hot 벡터로 변환
 3) sliding window 방식으로, window size 만큼을 학습. 예를 들어 window size가 3이라면, (I, study), (study, I), (study, math) 등의 train set 을 가짐

### Word2Vec 해보기
https://ronxin.github.io/wevi/ : config 조절해서 Word2Vec의 시각화

### Word2Vec의 결과
일관된 벡터 방향으로 단어 사이의 관계가 효과적으로 학습됨
![image](https://user-images.githubusercontent.com/43736669/109978198-f9f69d80-7d40-11eb-8450-20830c295522.png)

### Word2Vec의 활용
다양한 자연어 처리에서 널리 활용됨 
 - 기계 번역 : 다른 언어의 같은 의미를 가지는 단어 벡터가 서로 align 되게 해서 번역을 쉽게 도와줌
 ![image](https://user-images.githubusercontent.com/43736669/109978507-4c37be80-7d41-11eb-8cde-85b7c8411fc3.png)  
 - 감정 분석 : 각 단어의 긍/부정의 의미를 보다 효율적으로 파악할 수 있게 해줌 
 - Image Caption : 이미지의 상황을 파악하고 설명하는 모델에서도 이용

## GloVe(복습 필요)
