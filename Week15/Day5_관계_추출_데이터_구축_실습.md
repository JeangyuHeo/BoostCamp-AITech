# 관계 추출 데이터 구축 실습

<br>

## 과제 정의

### 과제 정의 시 고려할 요소

* 과제의 목적 
* 데이터 구축 규모 
* 원시 데이터 
* 데이터의 주석 체계 
* 데이터 주석 도구 
* 데이터의 형식 
* 데이터 검수 
* 데이터 평가

<br>

### 과제의 목적

관계 추출(Relataion Extraction)이란 문장에 등장하는 두 개체 간의 관계를 주석하는 것이다. 관계 추출의 대상이 되는 개체명을 인식하고, 각 개체가 주체(subject)인지 대상(object)를 파악한 뒤 그 둘 간의 관계를 주석한다. 주체와 대상, 관계로 이루어진 트리플(triplet)을 완성한다.



>특정한 도메인에 맞추어 관계 분류(Class) 목록을 확장하고, 확장된 관계를 주석한 데이터를 만든다.

<br>

### 데이터 구축 규모

기존 데이터의 규모

<img width="547" alt="Screen Shot 2021-11-12 at 10 50 46 PM" src="https://user-images.githubusercontent.com/88299729/141478881-02e5584c-bfb3-4493-8d78-e5058a6f2131.png">

<br>

### 원시 데이터

기존 데이터의 출처 

* TACRED 
  * TAC KBP challenge 2009~2014 
    * Train2009~2012,Dev2013,Test2014 
* KLUE 
  * WIKIPEDIA, WIKITREE, 정책브리핑



> 둘 이상의 개체와 개체 간의 관계를 추출할 만한 문장이 포함된 텍스트 선정

<br>

### 데이터 주석 체계

<img width="637" alt="Screen Shot 2021-11-12 at 10 52 55 PM" src="https://user-images.githubusercontent.com/88299729/141478950-8aae706d-d835-4fb0-bf0f-2d459c5ad26d.png">

<br>

### 데이터 주석 도구

* 주석 단계 세분화 후, 주석 도구 결정 
* 트리플(Triplet) 형태의 주석이 가능한 도구 선정 필요



<img width="535" alt="Screen Shot 2021-11-12 at 10 53 44 PM" src="https://user-images.githubusercontent.com/88299729/141479013-66c5ada8-d882-4547-befd-1dd23c7261ca.png">



#### e.g. TACRED

<img width="378" alt="Screen Shot 2021-11-12 at 10 54 25 PM" src="https://user-images.githubusercontent.com/88299729/141479051-e5ae4668-d139-4e72-a6f3-ccbce077edb6.png">

#### e.g. KLUE

<img width="360" alt="Screen Shot 2021-11-12 at 10 54 35 PM" src="https://user-images.githubusercontent.com/88299729/141479069-7fa2bcea-f225-44de-a911-73991563c034.png">

<br>

### 데이터 형식 - TACRED, JSON

<img width="387" alt="Screen Shot 2021-11-12 at 10 55 49 PM" src="https://user-images.githubusercontent.com/88299729/141479110-3d336681-a0b7-4bc1-b012-839b03750bdc.png">

<br>

### 데이터 형식 - KLUE

<img width="342" alt="Screen Shot 2021-11-12 at 10 56 01 PM" src="https://user-images.githubusercontent.com/88299729/141479137-740a3c3d-e85f-476d-a12c-325259ab89bc.png">

<br>

### 데이터 검수

* 데이터 형식의 정확도
* 관계 레이블의 정확도
* 관계 추출 정확도

> 검수 규모 정하기 : 전수 또는 특정 비율

<br>

### 데이터 평가

* 작업자간 일치도(IAA, Inter-AnnotatorAgreement)
  * Fleiss’ k (TACRED) 
  * Krippendorff’s α(KLUE) 
* 모델 성능 평가
  * 정밀도(Precision), 재현율(Recall), F1 (TACRED) 
  * Micro F1, AUPRC(areaundertheprecisionrecall curve) (KLUE)

<br>

<br>

## 구축 프로세스 설계

<img width="612" alt="Screen Shot 2021-11-12 at 10 58 29 PM" src="https://user-images.githubusercontent.com/88299729/141478838-50dd74fb-0889-4bc6-9697-d672cd61071e.png">

<img width="583" alt="Screen Shot 2021-11-12 at 10 59 41 PM" src="https://user-images.githubusercontent.com/88299729/141478855-96a8ce19-db3a-480c-8d2a-659690e50f98.png">

<br>

<br>

## 가이드라인 작성

#### 핵심 내용 : 주석 작업을 위한 가이드라인

* 작업 목적 
* 작업 도구 사용법 
* 작업 대상 문장과 아닌 문장 구분 기준 
* 레이블 별 주석 기준