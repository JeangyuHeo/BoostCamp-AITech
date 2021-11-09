# 자연어처리 데이터 소개 1



## 국내 언어 데이터의 구축 프로젝트

![화면 캡처 2021-11-10 021339](https://user-images.githubusercontent.com/88299729/140974803-91d9fa58-24b7-4f6e-bbc5-b5f835ccb552.png)

## 21세기 세종 계획과 모두의 말뭉치



### 21세기 세종 계획

‘21세기 세종계획’은 1997년에 그 계획이 수립되었고 이듬해인 1998년부터 2007년까지 10년 동안 시행된 한국의 국어 정보화 중장기 발전 계획(홍윤표,2009) 총 2억 어절의 자료 구축, 공개 XML형식, 언어정보나눔터 누리집을 통해 배포하다 중단 후 DVD로만 배포

<img src="https://user-images.githubusercontent.com/88299729/140974829-e28bad36-f0d2-466a-a5e5-fb7a2b27f0da.png" alt="화면 캡처 2021-11-10 022104" style="zoom:60%;" /><img src="https://user-images.githubusercontent.com/88299729/140974850-e7bba4f9-e20f-4056-8221-4a9ff0e03cf4.png" alt="화면 캡처 2021-11-10 022235" style="zoom:60%;" />

* <head>.* </head> : 제목

* < p > : paragraph, 단락, 절

* <u> : utterance 발화
* <who> : 발화자
* s : 억양 단위 표시, n을 이용하여 일련 번호 붙임
* desc : description

### 모두의 말뭉치

인공지능의 한국어 처리 능력 향상에 필수적인 한국어 학습 자료 공개 플랫폼.‘21세기 세종계획’에 비해 일상 대화,메신저,웹 문서 등 구어체 자료의 비중을 높임.다층위 주석 말뭉치 포함(형태, 구문, 어휘 의미, 의미역, 개체명, 상호 참조 등) JSON 형식, 모두의 말뭉치 누리집(https://corpus.korean.go.kr/)에서 배포



> Train, validation, Test set으로 나뉘어져 있지 않아 사용자가 직접 나누어야 한다.



* 원시 말뭉치와 주석 말뭉치로 구성

![화면 캡처 2021-11-10 022501](https://user-images.githubusercontent.com/88299729/140974962-c363642c-8b8d-430e-bc01-e9e89b198bc8.png)



## 엑소브레인 - ExoBrain

* 내몸 바깥에 있는 인공 두뇌

![화면 캡처 2021-11-10 022727](https://user-images.githubusercontent.com/88299729/140974989-f3065c07-04a6-48c9-b977-40c3caef6549.png)

* 엑소브레인은 인간의 지적 노동을 보조할 수 있는 언어처리 분야의 AI기술개발을 위해,전문직 종사자(예: 금융,법률,또는 특허 등)의 조사·분석 등의 지식노동을 보조 가능한 
  * 언어 문법 분석을 넘어선 언어의 의미 추론 기술 개발
  * 전문분야 원인,절차,상관관계 등 고차원 지식 학습 및 축적 기술 개발
  *  전문분야 대상 인간과 기계의 연속적인 문답을 통한 심층질의응답 기술 개발 및 국내외 표준화를 통해 핵심 IPR을 확보하는 우리나라 대표 인공지능 국가 R&D프로젝트.



* 21세기 세종 계획에서 개발된 주석 말뭉치의 체계를 확장하고 추가하여 TTA표준안 마련(형태,구문, 개체명)



## AI hub

![화면 캡처 2021-11-10 022832](https://user-images.githubusercontent.com/88299729/140975027-f255ce21-3cb7-420c-a86e-b12e1ff8c0dd.png)

* AI허브는 AI기술 및 제품·서비스 개발에 필요한 AI인프라(AI데이터, AISWAPI, 컴퓨팅 자원)를 지원하는 누구나 활용하고 참여하는 AI 통합 플랫폼
* 데이터별로 데이터 설명서,구축활용 가이드 제공 
* JSON,엑셀 등 다양한 형식의 데이터 제공
* 실제 산업계 수요 조사를 반영하여 다양한 TASK를 수행할 수 있는 자원 구축



## 민간 주도 데이터셋

### KLUE

![화면 캡처 2021-11-10 023043](https://user-images.githubusercontent.com/88299729/140975140-68aebf3e-99ed-4d6b-8a1b-5f60eb58c930.png)

한국어 이해 능력 평가를 위한 벤치마크 

* 뉴스 헤드라인 분류 
* 문장 유사도 비교 
* 자연어 추론 
* 개체명 인식 
* 관계 추출 
* 형태소 및 의존 구문 분석 
* 기계 독해 이해 
* 대화 상태 추적



### KorQuAD 1.0 & 2.0

![화면 캡처 2021-11-10 023054](https://user-images.githubusercontent.com/88299729/140975167-5b6926fd-79ae-47e7-8bb2-521a9a93bbf2.png)

* KorQuAD 2.0은 KorQuAD 1.0에서 질문답변 20,000+ 쌍을 포함하여 총 100,000+ 쌍으로 구성된 한국어 기계 독해(Machine Reading Comprehension)데이터셋
* 스탠포드 대학교에서 공개한 SQuAD(https://rajpurkar.github.io/SQuADexplorer/)를 벤치마킹 CCBY-ND2.0KR

### KorNLU

![화면 캡처 2021-11-10 023106](https://user-images.githubusercontent.com/88299729/140975174-b92df914-4651-4d7d-825d-85e2bd5da169.png)

영어로 된 자연어 추론(NLI,Natural language inference)및 문장 의미 유사도(STS,semantic textual similarity)데이터셋을 기계 번역하여 공개