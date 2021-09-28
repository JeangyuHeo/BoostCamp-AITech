## 인공지능과 자연어 처리

### 인공지능의 탄생과 자연어처리

인공지능과 자연어처리에 대해 소개합니다.

<br>

#### 자연어처리 소개

* 피그말리온과 갈리테이아 (B.C.43­ A.D.17)

  ![화면 캡처 2021-09-29 003406](https://user-images.githubusercontent.com/88299729/135127486-3b535d06-b6ee-4aef-b9d6-556ee34d48f5.png)

  * 피그말리온이 여성의 결점을 제거해서 만든 조각상
  * 인간을 대체하는 인공물에 대한 최초의 기록

![화면 캡처 2021-09-29 003519](https://user-images.githubusercontent.com/88299729/135127549-84d80e50-5467-4f3d-b846-ff6b7d1665bb.png)


* 콜로서스 컴퓨터 (1943)

  ![화면 캡처 2021-09-29 003544](https://user-images.githubusercontent.com/88299729/135127602-6976eecb-81bd-4e47-a351-bdf0c6c6228d.png)

  * 프로그래밍이 가능한 세계 최초의 전자식 컴퓨터 
  * 1500개의 진공관을 이용해 Boolean 논리 연산을 수행

  

* 이미테이션 게임 (튜링 테스트,1950)

  ![화면 캡처 2021-09-29 010425](https://user-images.githubusercontent.com/88299729/135127727-061a4003-25b1-4578-80df-de1cce46e420.png)

  * 기계에 지능이 있는지를 판별하고자 하는 실험 
  * 인간의 정의나 인간의 지능을 정의하긴 어렵다! 
  * 하지만,인간이 보기에 인간 같은 것을 인간에 준하는 지능이 있다고 간주 
  * 컴퓨터가 인간처럼 대화를 할 수 있다면 그 컴퓨터는 인간처럼 사고할 수 있다.



* AI의 황금기 (1956-1974)

  ![화면 캡처 2021-09-29 010440](https://user-images.githubusercontent.com/88299729/135127756-809e666e-0b8b-40e8-97ba-7a4113fb95cf.png)

  * Generalpurpose AI를 만들기 위해 자연어 연구가 폭발적으로 관심을 받게 됨 
  * 대표적인 **ELIZA(1966) **챗봇 
  * 심리 상담사의 역할을 하도록 설계 
  * 나 지금 너무 우울해 -> 왜 우울하세요? 
  * 가족 문제로 고민이야 -> 가족에 대해서 말해주세요. 
  * 최초의 대화형 (chitchat)챗봇 
  * 튜링 테스트를 적용할 수 있는 최초의 Human-Like AI

  ![화면 캡처 2021-09-29 010758](https://user-images.githubusercontent.com/88299729/135127847-9a441ea3-fbce-47ae-a4ae-905120b080c3.png)



#### 자연어처리의 응용분야

![화면 캡처 2021-09-29 010522](https://user-images.githubusercontent.com/88299729/135127783-199bf434-c5e3-472e-a2fb-c76c3f42e305.png)

* 컴퓨터의 응답 과정

  ![화면 캡처 2021-09-29 010841](https://user-images.githubusercontent.com/88299729/135128080-8076ed7a-44de-477e-9577-d8a869ece907.png)



* 인간의 대화 과정

![화면 캡처 2021-09-29 010827](https://user-images.githubusercontent.com/88299729/135127891-fc9961cc-289c-409e-b137-8923f8d5c400.png)

#### 자연어 단어 임베딩

![화면 캡처 2021-09-29 011238](https://user-images.githubusercontent.com/88299729/135128163-7f20b19d-e669-4e67-9b23-1cfcb8f8cd4f.png)

* Word2Vec

  * 가장 단순한 표현 방법은 one-hot encoding 방식 -> Sparse representation
  * 한 단어의 주변 단어들을 통해,그 단어의 의미를 파악

* FastText

  ![화면 캡처 2021-09-29 011324](https://user-images.githubusercontent.com/88299729/135128207-e04e7493-1c21-4a64-82f3-1a24fdf826c4.png)

  * FastText는 단어를 n-gram으로 분리를 한 후,모든 n-gram vector를 합산한 후 평균을 통해 단어 벡터를 획득
  * 오탈자,OOV,등장 회수가 적은 학습 단어에 대해서 강세

* 한계점

  * Word2Vec이나 FastText와 같은 word embedding 방식은 동형어,다의어 등에 대해선 embedding 성능이 좋지 못하다는 단점이 있음 
  * 주변 단어를 통해 학습이 이루어지기 때문에, ‘문맥’을 고려할 수 없음

### 딥러닝 기반의 자연어처리와 언어모델

#### 언어모델

* 모델이란?

  * 모델의 종류
    * 일기예보 모델,데이터 모델,비즈니스 모델,물리 모델,분자 모델 등
  * 모델의 특징
    * 자연 법칙을 컴퓨터로 모사함으로써 시뮬레이션이 가능 
    * 이전 state를 기반으로 미래의 state를 예측할 수 있음 (e.g.습도와 바람 세기 등으로 내일 날씨 예측)
    * 즉,미래의 state를 올바르게 예측하는 방식으로 모델 학습이 가능함

* Markov 기반의 언어모델

  ![화면 캡처 2021-09-29 011724](https://user-images.githubusercontent.com/88299729/135128262-3922efd7-2b49-49d3-b059-66c4a2020c57.png)

  * 마코프 체인 모델 (Markov Chain Model) 
  * 초기의 언어 모델은 다음의 단어나 문장이 나올 확률을 통계와 단어의 n-gram을 기반으로 계산 
  * 딥러닝 기반의 언어모델은 해당 확률을 최대로 하도록 네트워크를 학습

* Recurrent Neural Network(RNN)기반의 언어모델

  ![화면 캡처 2021-09-29 012014](https://user-images.githubusercontent.com/88299729/135128301-f3a4ae21-2544-4d50-a70c-42dba654780c.png)

  * RNN은 히든 노드가 방향을 가진 엣지로 연결돼 순환구조를 이룸 (directed cycle) 

  * 이전 state 정보가 다음 state를 예측하는데 사용됨으로써,시계열 데이터 처리에 특화

  * 마지막 출력은 앞선 단어들의 ‘문맥’ 을 고려해서 만들어진 최종 출력 vector -> Context vector 

  * 출력된 context vector 값에 대해 classification layer를 붙이면 문장 분류를 위한 신경망 모델

    ![화면 캡처 2021-09-29 012124](https://user-images.githubusercontent.com/88299729/135128378-cd73242b-5800-4360-9654-2f8cbcf36d70.png)

#### Seq2Seq

![화면 캡처 2021-09-29 012238](https://user-images.githubusercontent.com/88299729/135128428-04da8e35-8032-4886-9b43-b045c67b36c3.png)

* 구조
  * Encoder layer : RNN 구조를 통해 Context vector 를 획득 
  * Decoder layer : 획득된 Context vector를 입력으로 출력을 예측
* RNN 구조의 문제점
  * 입력 sequence의 길이가 매우 긴 경우,처음에 나온 token에 대한 정보가 희석 
  * 고정된 context vector 사이즈로 인해 긴 sequence에 대한 정보를 함축하기 어려움 
  * 모든 token이 영향을 미치니,중요하지 않은 token도 영향을 줌

#### Attention

![화면 캡처 2021-09-29 012510](https://user-images.githubusercontent.com/88299729/135128468-661b8aee-2dad-40f5-b20e-5813ac88b382.png)

* 아이디어

  * 인간이 정보처리를 할 때,모든 sequence를 고려하면서 정보처리를 하는 것이 아님 
  * 인간의 정보처리와 마찬가지로,중요한 feature는 더욱 중요하게 고려하는 것이 Attention의 모티브
  * 문맥에 따라 동적으로 할당되는 encode의 Attention weight로 인한 dynamic context vector를 획득 
  * 기존 Seq2Seq의 encoder,decoder 성능을 비약적으로 향상시킴

  

#### Self-attention

* 동작 과정

<img src="https://user-images.githubusercontent.com/88299729/135128740-eb014d91-598b-42db-893f-f19cb301e16c.png" alt="화면 캡처 2021-09-29 012603" style="zoom:80%;" /> <img src="https://user-images.githubusercontent.com/88299729/135128581-93575960-6352-4b22-b8c9-0de5379675fe.png" alt="화면 캡처 2021-09-29 012612" style="zoom:80%;" />



* 모델 구조

![화면 캡처 2021-09-29 012626](https://user-images.githubusercontent.com/88299729/135128888-61b0cfec-5687-4449-97bd-ca33b1c17896.png)

