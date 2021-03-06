## BERT 언어모델 기반의 단일 문장 분류

### KLUE 데이터셋 소개

KLUE 데이터셋을 소개합니다.



#### KLUE 데이터셋

* 한국어 자연어 이해 벤치마크(KoreanLanguageUnderstandingEvaluation,KLUE)

* 살면서 직면하게 되는 거의 모든 자연어 task 유형을 포함

  * 단일 문장 분류 task
    * 문장 분류
    * 관계 추출
  * 문장 임베딩 벡터의 유사도 (e.g. [CLS])
    * 문장 유사도
  * 두 문장 관계 분류 task
    * 자연어 추론
  * 문장 토큰 분류 task
    * 개체명 인식
    * 품사 태깅
    * 질의 응답
  * 목적형 대화
  * 의존 구문 분석

  

#### 의존구문분석

![화면 캡처 2021-09-30 025801](https://user-images.githubusercontent.com/88299729/135327574-1fa42e18-2e56-4b3f-b204-82767fa6b004.png)

단어들 사이의 관계를 분석하는 task

* 특징
  * 지배소 : 의미의 중심이 되는 요소
  * 의존소 : 지배소가 갖는 의미를 보완해주는 요소 (수식)
  * 어순과 생략이 자유로운 한국어와 같은 언어에서 주로 연구된다.
* 분류 규칙
  * 지배소는 후위언어이다. 즉, 지배소는 항상 의존소보다 뒤에 위치한다.
  * 각 의존소의 지배소는 하나이다.
  * 교차 의존 구조는 없다.

* 분류 방법

  ![화면 캡처 2021-09-30 025851](https://user-images.githubusercontent.com/88299729/135327648-a9a5c210-8bcb-4934-8d7d-195a2acc5ae3.png)

  

  * sequence labeling 방식으로 처리 단계를 나눈다.
  * 앞 어절에 의존소가 없고 다음 어절이 지배소인 어절을 삭제하며 의존 관계를 만든다.

* 사용 분야

  ![화면 캡처 2021-09-30 030324](https://user-images.githubusercontent.com/88299729/135327711-d2920401-d584-41d3-9c28-8116f65ebfc6.png)

  * 복잡한 자연어 형태를 그래프로 구조화해서 표현 가능! 각 대상에 대한 정보 추출이 가능!
  * ex1) '나'는 '구름그림'을 그렸다. , ex2) '구름 그림'은 '새털구름'을 그린 것이다.



### 단일 문장 분류 TASK 소개

#### 문장 분류 TASK

* **감정분석 (Sentiment Analysis)**
  * 문장의 긍정 또는 부정 및 중립 등 성향을 분류하는 프로세스
  * 문장을 작성한 사람의 느낌,감정 등을 분석 할 수 있기 때문에 기업에서 모니터링,고객지원,또는 댓글에 대한 필터링 등을 자동화하는 작업에 주로 사용
* 활용 방안
  * 혐오 발언 분류 : 댓글,게임 대화 등 혐오 발언을 분류하여 조치를 취하는 용도로 활용
  * 기업 모니터링 : 소셜, 리뷰 등 데이터에 대해 기업 이미지, 브랜드 선호도, 제품평가 등 긍정 또는 부정적 요인을 분석
* **주제 라벨링 (Topic Labeling)**
  * 문장의 내용을 이해하고 적절한 범주를 분류하는 프로세스
  * 주제별로 뉴스 기사를 구성하는 등 데이터 구조화와 구성에 용이
* 활용 방안
  * 대용량 문서 분류 :대용량의 문서를 범주화
  * VoC (Voice of Customer) : 고객의 피드백을 제품 가격, 개선점, 디자인 등 적절한 주제로 분류하여 데이터를 구조화
* **언어감지 (Language Detection)**
  * 문장이 어떤 나라 언어인지를 분류하는 프로세스
  * 주로 번역기에서 정확한 번역을 위해 입력 문장이 어떤 나라의 언어인지 타켓팅 하는 작업이 가능
* 활용 방안
  * 번역기 : 번역할 문장에 대해 적절한 언어를 감지함
  * 데이터 필터링 : 타겟 언어 이외 데이터는 필터링
* **의도 분류 (Intent Classification)**
  * 문장이 가진 의도를 분류하는 프로세스
  * 입력 문장이 질문,불만,명령 등 다양한 의도를 가질 수 있기 때문에 적절한 피드백을 줄 수 있는 곳으로 라우팅 작업이 가능
* 활용 방안
  * 챗봇 : 문장의 의도인 질문, 명령, 거절 등을 분석하고 적절한 답변을 주기 위해 활용



#### 문장 분류를 위한 데이터

* Kor_hate 
  * 혐오 표현에 대한 데이터
  * 특정 개인 또는 집단에 대한 공격적 문장 
  * 무례, 공격적이거나 비꼬는 문장 
  * 부정적이지 않은 문장
* Kor_sarcasm 
  * 비꼬지 않은 표현의 문장 
  * 비꼬는 표현의 문장
* Kor_sae 
  * 예/아니오로 답변 가능한 질문 
  * 대안 선택을 묻는 질문 
  * Wh- 질문 (who, what, where, when, why, how) 
  * 금지 명령 
  * 요구 명령 
  * 강한 요구 명령
* Kor_3i4k 
  * 단어 또는 문장 조각 
  * 평서문 
  * 질문 
  * 명령문 
  * 수사적 질문 
  * 수사적 명령문 
  * 억양에 의존하는 의도

### 단일 문장 분류 모델 학습

#### 모델 구조도

![화면 캡처 2021-09-30 031604](https://user-images.githubusercontent.com/88299729/135327748-f7d859b4-e7fd-4ec9-85a3-2d1f32105ef1.png)

#### 학습 과정

![화면 캡처 2021-09-30 031619](https://user-images.githubusercontent.com/88299729/135327773-467f0ee2-f962-4c45-9d79-0d37e22e1ad8.png)