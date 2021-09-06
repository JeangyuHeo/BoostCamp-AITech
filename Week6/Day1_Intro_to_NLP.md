## Intro to NLP



### Natural Language Processing

#### 주요 학회

* ACL
* EMNLP
* NAACL



#### Low level parsing

* Tokenization

  문장에서 의미 단위로 쪼개는 task를 의미한다.

* stemming

  어근과 어미가 있을 때, 어근들만 판별해 내는 task를 의미한다.



#### Word and phrase level

* NER (Named Entity Recognition)

  단일 단어, 여러 단어, 또는 고유 명사를 인식하는 task 이다.

* POS (Part-Of-Speech)

  단어들의 성분이 무엇인지, 형용사인지, 부사인지, 동사인지 등을 알아내는 task 이다.



#### Sentence level

* Sentiment analysis

  문장이 긍정적인지, 부정적인지 파악하는 task이다.

  ex) This movie was not that bad. (긍정)

* machine translation

  이름에서 쉽게 알 수 있듯이 번역 작업을 하는 task이다.

  * 문장을 전체적으로 이해한 다음 번역하고자 하는 언어의 어순과 단어를 적절히 사용해서 번역해야한다.



#### Multi_sentence and paragragh level

* Entailment prediction

  논리적으로 양립 할 수 있는지 없는지를 판별하는 task이다.

* Question answering

  질문에 대한 답변을 얻는 task이다.

  ex) Google에서 Where did Napoleon die? 라고 검색하면 페이지로 안내하는 것이 아닌 질문에 대한 대답을 얻을 수 있다.

* Dialog system

  chat bot과 같이 대화를 주고 받을 수 있는 task이다.

* Summarization

  어떠한 내용을 가진 글이 있을 때, 한줄 요약의 형태로 답변을 얻는 형태의 task이다.



#### Text mining (학회 : The WebConf, WSDM, KDD)

* text data에서 **필요한 데이터만을 추출**하는 task
* 데이터를 긁어서 모아올 때, 비슷한 의미를 가진 키워드끼리 grouping 해서 분석 할 필요가 생긴다. 이를 자동을 해주는 **topic modeling**이 있다.



####  Information retrieval (학회 : SIGIR, WSDM, CIKM, RecSys)

네이버가 하고 있는 **검색 기술** 연구와 관련이 있다. 이는 추천 시스템과 밀접한 관련이 있어 함께 접목하여 사용하면 좋다.



> 자연어 처리

​	text data를 단어 단위로 분리하고 각 단어를 특정한 dimension으로 이루어진 벡터로 표현하는 과정을 거친다.



#### Word embedding

* 각 단어를 특정한 차원으로 이루어진 공간 상의 한점(그 점의 좌표)으로 나타내주는 기법을 의미한다.
* 비슷한 의미를 가진 단어가 비슷한 위치에 있음으로서 단어 의미 상의 유사도를 잘 반영한 벡터 표현을 자연어 처리 알고리즘에게 전해준다.



#### Bag-of-Words (NaiveBayes Classifier)

![화면 캡처 2021-09-06 221319](https://user-images.githubusercontent.com/88299729/132226155-b7249c8a-ec73-45f9-9000-af8af191c0c3.png)

![화면 캡처 2021-09-06 221336](https://user-images.githubusercontent.com/88299729/132226237-f401127c-f0c1-4152-a9b8-5a32654360fc.png)

![화면 캡처 2021-09-06 221352](https://user-images.githubusercontent.com/88299729/132226268-42707b9d-1072-44b2-a6b9-a047adc90a9b.png)



* 8개의 단어가 있다고 가정했을 때, 8개의 공간(vector)을 만든다.
* 각 단어에 대해서 각 차원을 맵핑하고 원핫 벡터로 표현한다.
* 8개의 dimension으로 문장의 각 단어를 표현한다.
* 모든 벡터를 더하면 bag-of-words가 된다.



![화면 캡처 2021-09-06 221724](https://user-images.githubusercontent.com/88299729/132226300-ecda2736-38db-4dd7-97ec-8e6a651eb2d9.png)

![image](https://user-images.githubusercontent.com/88299729/132226487-e2ec27f7-fcb3-4d63-a881-5d9ba60296f8.png)

![화면 캡처 2021-09-06 222440](https://user-images.githubusercontent.com/88299729/132226375-9f5831de-598e-408f-8b4a-af1611fa47c8.png)



#### Word2Vec



![화면 캡처 2021-09-06 223758](https://user-images.githubusercontent.com/88299729/132226531-9823834c-828c-4e0b-81bf-3c29f9e65811.png)



* 인접한 단어들 간의 의미가 비슷할 거라는 가정 하에 진행된다.
* sliding window 기법을 사용해서 input, output 단어 쌍을 구한다. (word2Vec 학습 데이터를 구성하는 것)
* 비슷한 논리의 예를 들어 남자,여자, 삼촌, 이모, 왕, 왕비 등은 같은 벡터 형태를 보인다.



![화면 캡처 2021-09-06 223817](https://user-images.githubusercontent.com/88299729/132226568-b320aee1-b289-4ef6-9d6c-b256af939acf.png)



#### word intrusion detection
* 여러 단어들 중에 나머지 단어와 가장 의미가 상이한 하나를 찾는 task 이다.
* 모든 단어 간의 유클리드 거리를 구하고, 평균 값을 낸 후에 그것과의 거리가 가장 큰 것이 상이하다.



#### GloVe Model

![화면 캡처 2021-09-06 224038](https://user-images.githubusercontent.com/88299729/132226591-0ef9d78b-6bf4-45ac-9be6-6f21c088f9d6.png)



* 입력, 출력 각 단어 쌍들에 대해서 학습 데이터 안에서 한 윈도우 내에서 총 몇번 동시에 등장했는지 사전에 미리 계산한다.
* embedding vector ui 와 출력 word 의 vj 간의 내적 값에 확률의 로그 값을 빼줌으로서 더 잘 수렴 할 수 있는 loss func 을 이용한다.

