## BERT 언어 모델 기반의 문장 토큰 분류

### 문장 토큰 분류 task

![화면 캡처 2021-10-01 234106](https://user-images.githubusercontent.com/88299729/135647392-def24fe5-4db3-44be-b189-394744a4a0b1.png)

주어진 문장의 각 token이 어떤 범주에 속하는지 분류하는 task

#### task 소개

* **Named Entity Recognition (NER)**

  ![화면 캡처 2021-10-01 234315](https://user-images.githubusercontent.com/88299729/135647492-e9c37575-b810-4e6d-8f84-b11cad93ee58.png)

  * 개체명 인식은 문맥을 파악해서 인명, 기관명, 지명 등과 같은 문장 또는 문서에서 특정한 의미를 가지고 있는 단어 또는 어구(개체) 등을 인식하는 과정을 의미한다.

    ![화면 캡처 2021-10-02 002309](https://user-images.githubusercontent.com/88299729/135647524-9a94af2a-40c5-4cdc-b8e3-c86441a108e7.png)

* **Part-of-speech tagging (POS TAGGING)**

  ![화면 캡처 2021-10-02 002745](https://user-images.githubusercontent.com/88299729/135647581-21519900-36a2-472d-a7ee-4be71bc3bb32.png)

  * 품사란 단어를 문법적 성질의 공통성에 따라 언어학자들이 몇 갈래로 묶어 놓은 것이다. 
  * 품사 태깅은 주어진 문장의 각 성분에 대하여 가장 알맞는 품사를 태깅하는 것을 의미한다.

  ![화면 캡처 2021-10-02 002813](https://user-images.githubusercontent.com/88299729/135647610-6c289678-d838-4b14-bc27-9e7c29233663.png)

#### 데이터 소개

* **kor_ner**

  ![화면 캡처 2021-10-02 002903](https://user-images.githubusercontent.com/88299729/135647631-3b32c99c-c78b-49b5-b057-bb811c6ca3ec.png)

  * 한국해양대학교 자연어 처리 연구실에서 공개한 한국어 NER 데이터셋 

  * 일반적으로, NER 데이터셋은 pos tagging 도 함께 존재

    ![화면 캡처 2021-10-02 003040](https://user-images.githubusercontent.com/88299729/135647659-4c8b7c98-2c1c-47e7-bee2-3f46dc549626.png)

  * Entity tag에서 B의 의미는 개체명의 시작(Begin)을 의미하고, I의 의미는 내부(Inside)를 의미하며, O는 다루지 않는 개체명(Outside)를 의미한다. 

  * 즉, B-PER은 인물명 개체명의 시작을 의미하며, I-PER는 인물명 개체명의 내부 부분을 뜻한다. 

  * kor_ner 데이터셋에서 다루는 개체명은 다음과 같다.



### 문장 토큰 분류 모델 학습 실습

#### 문장 토큰 분류 모델 학습

![화면 캡처 2021-10-02 003100](https://user-images.githubusercontent.com/88299729/135647701-4f8c301b-731d-47e1-b01e-377ee66f7f06.png)



#### 주의점

![화면 캡처 2021-10-02 003115](https://user-images.githubusercontent.com/88299729/135647719-16e56543-3eac-44a1-9bba-a601358cf8fc.png)



#### 학습 과정

![화면 캡처 2021-10-02 003148](https://user-images.githubusercontent.com/88299729/135647761-f752872c-0626-4aed-8065-7dceb8fa6ffa.png)



