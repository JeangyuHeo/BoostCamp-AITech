# 관계 추출 과제의 이해

<img width="240" alt="Screen Shot 2021-11-12 at 9 55 45 PM" src="https://user-images.githubusercontent.com/88299729/141475640-f09fa674-9588-4f11-8991-6b3077e035a2.png"> <img width="531" alt="Screen Shot 2021-11-12 at 9 55 59 PM" src="https://user-images.githubusercontent.com/88299729/141475655-08994d3e-7adb-4918-9fa9-0fa5449fbd78.png">







## 관계 추출 관련 과제의 개요

### 개체명(Entity) 인식 NER, Named Entity Recognition

* 개체명이란 인명, 지명, 기관명 등과 같은 고유명사나 명사구를 의미.
* 개체명 인식 태스크는 문장을 분석 대상으로 삼아서 문장에 출현한 개체명의 경계를 인식하고, 각 개체명에 해당하는 태그를 주석함.
* KLUE에서는 국제적인 기준에서 가장 널리 알려진 CoNLL 2003의 태그 체계 및 Stanford NER을 바탕으로 국내 TTA 표준 지침의 주석 가이드라인에 따라 데이터를 구축함.
* PS(사람), LC(지역), OG(기관), DT(날짜), TI(시간), QT(수량)

<img width="521" alt="Screen Shot 2021-11-12 at 10 08 25 PM" src="https://user-images.githubusercontent.com/88299729/141475868-b300db1d-b831-46d0-988f-334a18e6a86b.png">

<img width="656" alt="Screen Shot 2021-11-12 at 10 08 52 PM" src="https://user-images.githubusercontent.com/88299729/141475899-8a3bcc1f-882e-4bc2-bc99-8296388dfe74.png">

#### output

<img width="612" alt="Screen Shot 2021-11-12 at 10 19 08 PM" src="https://user-images.githubusercontent.com/88299729/141476029-66ca6bcf-16e6-4900-9f4e-dee1641ec150.png">

<img width="615" alt="Screen Shot 2021-11-12 at 10 19 21 PM" src="https://user-images.githubusercontent.com/88299729/141476059-6fbfac95-7650-4d6f-beb9-4e560fd10a4e.png">

<img width="575" alt="Screen Shot 2021-11-12 at 10 19 41 PM" src="https://user-images.githubusercontent.com/88299729/141476072-5d776bce-b508-4218-b9fd-8345d79df3a6.png">

### 관계(Relation) 추출 RE, Relation Extract

* 관계 추출은 문장에서 나타난 개체명 쌍(Entity Pair)의 관계(Relation)을 판별하는 태스크. 
* 개체명 쌍은 관계의 주체(Subject)와 대상(Object)로 구성됨. 
* KLUE에서는 TACLED에 기반하여 30개 관계 Class를 설정하여 데이터를 구축함.

<img width="635" alt="Screen Shot 2021-11-12 at 10 15 16 PM" src="https://user-images.githubusercontent.com/88299729/141475953-60a3e8ef-bd01-47a9-825e-24c5e17b4e53.png">



#### output

<img width="637" alt="Screen Shot 2021-11-12 at 10 19 57 PM" src="https://user-images.githubusercontent.com/88299729/141476133-c01d12d6-a5ad-4e23-9700-1ff7910860d0.png">



<img width="513" alt="Screen Shot 2021-11-12 at 10 20 10 PM" src="https://user-images.githubusercontent.com/88299729/141476171-833a64a5-50ff-4965-937c-bd827f1acb0d.png">



### 개체명 연결 EL, Entity Linking

* 개체명을 인식(NamedEntityRecognition)하고 모호성을 해소(Named Entity Disambiguation)하는 과제를 결합한 것. 
* 텍스트에서 추출된 개체명을 지식 베이스(knowledge base)와 연결하여 모호성을 해소함.

* AIDA CoNLL-YAGO Dataset 또는 TAC KBP English Entity Linking Comprehensive and Evaluation Data 2010 등이 있음.

<img width="640" alt="Screen Shot 2021-11-12 at 10 18 05 PM" src="https://user-images.githubusercontent.com/88299729/141475975-abd54f06-93bb-4f6f-a48a-eb046b226d9d.png">



## 과제별 차이점

<img width="652" alt="Screen Shot 2021-11-12 at 10 21 09 PM" src="https://user-images.githubusercontent.com/88299729/141476202-aa997e3a-fa04-47b5-a8b0-9b34dc94581d.png">



## 데이터 제작시 문제점



### NER

* **2개 이상의 태그로 주석될 수 있는 개체명** → 맥락에 기반한 주석
  *  ex) 서울시는 정책을 발표했다. 
  * 그 카페는 서울시 서대문구 연희동에 있다. 
* **주석 대상의 범주** → 구체적 범주 및 기준 명시 
  * ex) A급, B급, C급, 삼류(3류)



### RE

* **한국어 데이터 현실에 맞지 않는 주석** → 태그 통폐합 및 추가 
  * ex) 지역 관련 태그 통합, 사람, 기관의 작품 및 생산물 관련 태그 추가
* **KB(Knowledge base)의 활용** → 일부만 활용



### EL

* **적합한 KB(Knowledgebase) 선정의 문제**
  * 현재 AI HUB에 공개된 KB의 경우 제한적인 저작권 아래서 활용이 가능함. 위키 데이터를 활용하여 자체적인 지식베이스를 구축하여 활용하거나, 서비스 도메인에 맞는 지식베이스를 구축하여 활용할 수 있음. 지식베이스를 구축하는 것 자체가 많은 비용과 자원이 드는 일이므로 이에 대한 대비가 필요함



### 이러한 데이터 만드는 이유?

* NER, RE, EL은 기본적으로 비구조화된 텍스트에서 정보를 추출하여 구조화하려는 것이 목적 

* 따라서 이 과정에서 지식 베이스가 활용되기도 하고, 이 결과물이 지식 베이스가 되기도 함 

* 정보 처리의 관점에서 구조화된 정보의 활용도가 높기 때문에 이러한 시도는 앞으로도 계속 될 것



### Knowledge Graph

<img width="588" alt="Screen Shot 2021-11-12 at 10 32 31 PM" src="https://user-images.githubusercontent.com/88299729/141476236-7e8c3975-a285-429f-aed1-91a3e0cec77a.png">

<img width="232" alt="Screen Shot 2021-11-12 at 10 32 43 PM" src="https://user-images.githubusercontent.com/88299729/141476352-722606ba-0a98-4f95-b75f-556cc5b6a7d2.png">

### NER, RE, EL의 활용

#### 검색 시스템

<img width="678" alt="Screen Shot 2021-11-12 at 10 33 20 PM" src="https://user-images.githubusercontent.com/88299729/141476369-731e438b-617f-4c2d-a2de-5aa2a3df8518.png">

#### HR 챗봇

<img width="529" alt="Screen Shot 2021-11-12 at 10 33 42 PM" src="https://user-images.githubusercontent.com/88299729/141476378-28c71151-c18e-44e2-a24b-b0bd1e5c1c29.png">

#### 구글 핀포인트

<img width="664" alt="Screen Shot 2021-11-12 at 10 35 09 PM" src="https://user-images.githubusercontent.com/88299729/141476395-2b1b09dc-1cd7-44bf-bee6-ddc4eb290721.png">

