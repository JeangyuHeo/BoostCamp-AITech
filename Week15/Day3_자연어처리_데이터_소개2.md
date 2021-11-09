# 자연어처리 데이터 소개2



## 질의 응답 Question Answering

### SQuAD

![화면 캡처 2021-11-10 023928](https://user-images.githubusercontent.com/88299729/140978032-b232d177-68c3-445d-9950-bad397db0c69.png)

위키피디아 데이터를 기반으로 제작한 기계 독해 및 질의응답 데이터



* **SQuAD1.0** **- 데이터 구축** 
  * 구축 대상 기사 추출 
    * 위키피디아 상위 10,000기사 중 500자 이하인 536 기사 무작위 추출 
  * 크라우드 소싱을 통한 질의 응답 수집 
    * 각 문단마다 다섯 개의 질문과 답변 수집 
  * 추가 응답 수집 
    * 평가를 통해서 각 질문 당 최소 두 개의 추가적인 답변 수집. 
    * 기사의 단락과 질문 노출 후 가장 짧은 대답 선택



* **SQuAD2.0- 데이터 구축**
  * 크라우드 소싱 플랫폼을 통한 대답하기 어려운 질문(unanswerable questions)수집 
    * 각 문단마다 각 문단 만으로는 대답할 수 없는 다섯 개의 질문 생성 
    * 적합한 질문을 25개 이하로 남김 
  * 적합한 질문이 수집되지 않은 기사 삭제 
  * 학습,검증,평가용 데이터 분할



## 기계 번역 Machine Translation

### WMT Dataset

2014년부터 시행된 기계 번역 학회에서 공개한 데이터셋 다국어 번역 데이터이며,두 언어간의 병렬 말뭉치로 구성됨.뉴스, 바이오, 멀티 모달 데이터 등이 제공됨



* **WMT데이터셋 - 데이터 구축 2018년 기준**
  * 평가용 데이터 :1,500개의 영어 문장을 다른 언어로 번역 +1,500개의 문장은 다른 언어에서 영어 문장으로 번역 
  * 훈련용 데이터 :기존에 존재하는 병렬 말뭉치와 단일 언어 말뭉치를 제공

## 요약 Text Summarization

### CNN/Daily Mail

* 추상 요약 말뭉치.
* 기사에 대하여 사람이 직접 작성한 요약문이 짝을 이루고 있음. 
* 학습 데이터 286,817쌍,검증 데이터 13,368쌍, 평가 데이터 11,487쌍으로 구성 
* 저작권 문제로 URLlist를 제공함



## 대화 Dialogue

### DSTC Dialog System Technology Challenges

#### DSTC1

human-computer dialogs in the bus timetable domain

#### DSTC2 and DSTC3

human-computer dialogs in the restaurant information domain

#### DSTC4 and DSTC5

DSTC4human-human dialogs in the tourist information domain

#### DSTC6 이후

End-to-End Goal Oriented Dialog Learning, End-to-End Conversation Modeling, and Dialogue Breakdown Detection로 확장

![화면 캡처 2021-11-10 024938](https://user-images.githubusercontent.com/88299729/140978053-52cc1a51-7ea9-4df2-ba60-c4b4469822ae.png)

### Wizard-of-Oz

* WoZ 방식으로 수집된 데이터셋이며 대화 상태 추적 데이터와 유사한 형태로 이루어짐 

* Woz 방식은 대화 수집 방식의 하나로,참여자가 대화 시스템을 통해 대화를 하고 있다고 생각하게 한 뒤 실제로는 실제 사람이 참여자의 발화에 맞추어 응답을 제시하고 대화를 이끌어나면서 대화를 수집하는 방식

![화면 캡처 2021-11-10 025030](https://user-images.githubusercontent.com/88299729/140978089-c563b809-a905-48b6-ac13-76404f9e88d3.png)

### UDC (Ubuntu Dialogue Corpus)

* 우분투 플랫폼 포럼의 대화를 수집한 데이터 
* 100만 개의 멀티 턴 대화로 구성,700만 개 이상의 발화와 1억개의 단어 포함 
* 특별한 레이블이 주석되어 있지 않음. 
* 대화 상태 추적과 블로그 등에서 보이는 비구조적 상호작용의 특성을 모두 가지고 있음

![화면 캡처 2021-11-10 025330](https://user-images.githubusercontent.com/88299729/140978108-cdf373c2-dadd-4776-8c35-868360c8bd40.png)