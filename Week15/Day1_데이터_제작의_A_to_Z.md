## 데이터 제작의 A to Z



* 인공지능 서비스 개발을 위한 데이터 제작 과정을 이해한다.

* 자연어처리 Task별 데이터의 특성을 탐구한다.
* 실습을 통해 실제 데이터 구축 과정을 체험한다.

<br>

#### 인공지능 서비스 개발 과정

<img width="602" alt="Screen Shot 2021-11-08 at 9 52 41 PM" src="https://user-images.githubusercontent.com/88299729/140749860-5b345931-b6ca-4cfc-b2f0-a899a3d5e5a7.png">

#### 데이터 구축 과정

<img width="595" alt="Screen Shot 2021-11-08 at 9 54 35 PM" src="https://user-images.githubusercontent.com/88299729/140749893-157d49d4-dc43-4ea3-84dd-6315158b04bd.png">

#### AI 데이터 설계의 구성 요소

* 데이터 설계
  * 데이터의 형식
  * 데이텅 표상 영역
* 데이터 수집-가공 설계
  * 원천 데이터 수집 방식
    * 전산화
    * 스크래핑
    * 작업자 작성
    * 모델 생성
  * 주석 작업
    * 전문가 구축
    * 크라우드 소싱



#### 데이터의 유형

<img width="583" alt="Screen Shot 2021-11-08 at 9 59 55 PM" src="https://user-images.githubusercontent.com/88299729/140749927-2ddcf39c-f309-4555-810a-ec7b8a21e758.png">

#### 데이터의 Input / Output 형식

* 텍스트 : HTML, XML, CSV, TSV, TXT, JSON, JSONL
* 이미지 : JPG, Jpeg, PDF, png, ocr
* 영상 : Wav, mp3, pcm, script



#### 데이터 (Train/Dev(Validation)/Test)별 규모와 구분(split) 방식

<img width="598" alt="Screen Shot 2021-11-08 at 10 07 29 PM" src="https://user-images.githubusercontent.com/88299729/140749972-aa9e166c-ed1a-4d0d-b010-d08b620e9b5a.png">

규모 선정에 필요한 정보 : 확보 가능한 원시 데이터의 규모, 주석 작업 시간

구분 방식 : 데이터 별 비율과 기준 정하기

랜덤 vs 특정 조건



#### 원시 데이터 수집 방식

전산화, 스크래핑, 작업자 작성, 모델 생성 : 적합한 데이터란 무엇인지 기준 세우기

<img width="555" alt="Screen Shot 2021-11-08 at 10 08 51 PM" src="https://user-images.githubusercontent.com/88299729/140749992-bc12a9e0-953d-4699-80b3-e831d12ef7c6.png">

#### 작업자 선정

주석 작업의 난이도와 구축 규모에 맞는 작업자 선정 및 작업 관리

<img width="445" alt="Screen Shot 2021-11-08 at 10 13 30 PM" src="https://user-images.githubusercontent.com/88299729/140750069-97c6ae75-bc04-4439-8f33-a90efd53fc4b.png">

#### 구축 및 검수 설계

구축 작업의 난이도와 구축 규모, 태스크 특성에 맞는 구축 및 검수 방식(전문가, IAA) 설계



* 파일럿
  * 설계시 발견하지 못한 이슈 발굴 및 해결
  * 가이드라인 보완 및 개정
  * 작업자 선정
* 본 구축
  * 작업 일정 관리
  * 작업자 관리
  * 중간 검수를 통한 데이터 품질 관리



#### 평가 지표 설정

* 전문가 평가 및 분석
  * 샘플링 검사
  * 가이드라인 적합도 분석
* 자동 평가 및 분석
  * 데이터 형식
  * 레이블별 분포 파악
  * 일괄 수정 사항 반영



#### 자연어와 인공어

<img width="578" alt="Screen Shot 2021-11-08 at 10 17 15 PM" src="https://user-images.githubusercontent.com/88299729/140750091-b11d73d6-9144-4459-8e23-9547cf2cc38d.png">

#### 자연어처리 (NLP, Natural Language Processing) 란?

인공지능의 한 분야, 사람의 언어를 컴퓨터가 알아듣도록 처리하는 인터페이스 역할

자연어 이해(NLU, Natural Language Understanding)와 자연어 생성(NLG, Natural Language Generation)으로 구성



> 자연어 처리의 최종 목표

컴퓨터가 사람의 언어를 이해하고 여러가지 문제를 수행할 수 있도록 하는 것



#### 자연어처리와 관련 연구 분야

<img width="405" alt="Screen Shot 2021-11-08 at 10 21 25 PM" src="https://user-images.githubusercontent.com/88299729/140750148-3504f07e-ac5a-48ea-b70c-f85401318446.png">

<img width="603" alt="Screen Shot 2021-11-08 at 10 21 48 PM" src="https://user-images.githubusercontent.com/88299729/140750200-cc52ee8f-231a-42b6-99c4-5996965c29eb.png">

#### 데이터 분류 방식

* 원천 데이터 장르(Domain)
  * 문어(가사, 도서 등), 구어(대화 등), 웹(메신저 대화, 게시판 등)



* Task의 유형
  * 자연어 이해(형태 분석, 구문 분석, 문장 유사도 평가 등)
  * 자연어 생성(기계 번역, 추상 요약 등)
  * 혼합(챗봇 등)



* 자연어처리 데이터를 만들 때는 복잡한 과제도 단순화 하여 단계별로 구축