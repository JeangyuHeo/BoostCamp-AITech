## BERT 언어모델 기반의 두 문장 관계 분류



### 두 문장 관계 분류 task소개

두 문장 관계 분류 task를 알아봅니다.

#### task 소개

![화면 캡처 2021-10-01 231106](https://user-images.githubusercontent.com/88299729/135635598-4bf9d982-7932-447f-a96e-8f43ca0fc092.png)

주어진 2개의 문장에 대해, 두 문장의 자연어 추론과 의미론적인 유사성을 측정하는 task



#### 데이터 소개

* **Natural Language Inference (NLI)**

  ![화면 캡처 2021-10-01 231556](https://user-images.githubusercontent.com/88299729/135635625-287f8734-eac6-41e3-9fb0-aa53a312c92f.png)
  )

* * 언어모델이 자연어의 맥락을 이해할 수 있는지 검증하는 task 
  * 전제문장(Premise)과 가설문장(Hypothesis)을 Entailment(함의), Contradiction(모순), Neutral (중립) 으로 분류

* **Semantic text pair**

  ![화면 캡처 2021-10-01 231701](https://user-images.githubusercontent.com/88299729/135635671-9f040fa6-fd54-4fa4-b20e-ef69b4ed47cf.png)

  * 두 문장의 의미가 서로 같은 문장인지 검증하는 task





### 모델 학습 실습

#### BERT를 이용한 챗봇 만들기

BERT를 활용해 IRQA(Information Retrieval Question and Answering) 챗봇을 만들어봅니다.



#### 시스템 구조도

![화면 캡처 2021-10-01 231817](https://user-images.githubusercontent.com/88299729/135635757-4726073f-4c81-4a21-809a-55c3ac3fe802.png)

