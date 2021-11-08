# 자연어처리 데이터 기초

## 1. 인공지능 모델 개발을 위한 데이터

### 데이터의 종류

![화면 캡처 2021-11-09 013434](https://user-images.githubusercontent.com/88299729/140785368-22540a9e-a2a4-458e-b1ac-998b8eea907e.png)

### 인공지능 기술의 발전

![화면 캡처 2021-11-09 013422](https://user-images.githubusercontent.com/88299729/140785378-9b80492d-838e-417e-850d-69db09d21c22.png)

### 언어 모델 평가를 위한 종합적인 벤치마크 등장

![화면 캡처 2021-11-09 013506](https://user-images.githubusercontent.com/88299729/140785393-a2f7ed70-d01d-443b-af18-3461de6d663c.png)

### 벤치마크의 구성

![화면 캡처 2021-11-09 013525](https://user-images.githubusercontent.com/88299729/140785429-9e8de3e8-3d32-4fa7-9fdc-25d880efcc16.png)

<br>

<br>

## 2. 데이터 관련 용어 정리



### 텍스트 (Text)

주석, 번역, 서문 및 부록 따위에 대한 본문이나 원문

언어 문장보다 더 큰 문법 단위, 문장이 모여서 이루어진 한 덩어리의 글을 이룬다.



### 말뭉치 corpus, plural corpora (복수형)

말뭉치(이상섭, 1988) : 어떤 기준으로든 한 덩어리로 볼 수 있는 말의 뭉치(한 저작자의 저작 전부, 특정 분야 저작 전체)

* 텍스트 아카이브
  * 일정한 규칙없이 텍스트들을 모아둔 것
* 말뭉치 corpus
  * 일정한 규칙을 가지고 디자인하여 텍스트들을 모아둔 것



### 데이터 (data)

* 정보 통신 컴퓨터가 처리할 수 있는 문자, 숫자, 소리, 그림 따위의 형태로 된 정보
* 말뭉치 데이터 (corpus data) : 말뭉치 자체
* 말뭉치의 데이터 (data from corpus) : 용례 색인 결과, 언어 추출 결과, 통계 분석 결과



### 주석

주석 : tag, label, annotation

주석하다 : tag, label, annotate



형태소 분석기 VS 형태소 주석기

* 영어는 POS( Part Of Speech) tagger 라고 한다.
* 한국어로는 형태소 분석기라고 한다. 
  * 언어적인 분석을 통해 주석을 다는 것이기 때문에 처음 명명을 분석기로 하였다.



### 언어학의 연구 분야

![화면 캡처 2021-11-09 014233](https://user-images.githubusercontent.com/88299729/140785455-685ea772-1504-456a-ad5a-d2770742647a.png)

### 텍스트 데이터의 기본 단위

* 영어 말 뭉치의 계량 단위 : 단어(= 띄어쓰기 단위) / 문장 또는 발화
* 한국어 말뭉치의 계량 단위 : 어절(=띄어쓰기 단위) / 문장 또는 발화



한국어의 "단어" : 9품사로 분석됨 명사, 수사, 대명사, 동사, 형용사, 관형사, 부사, 조사, 감탄사

이 중 "조사"는 체언(명사, 수사, 대명사)와 붙어서 사용되기 때문에 띄어쓰기 단위와 단어의 단위가 일치하지 않음

또한, "어미"는 하나의 품사로 인정되지 않으며 형태 단위이므로 독립된 단어가 아님



품사 : 단어를 문법적 성질의 공통성에 따라 몇 갈래로 묶어 놓은 것

품사 분류의 기준 : 의미(뜻, meaning), 기능(구실, function), 형식(꼴, form)



### 타입(type) & 토큰(token)

* 토큰화 tokenization
  * 표제어 추출 lemmatization
  * 품사 주석 POS(part ofspeech) tagging
* TTR:type/token ratio
  * 말뭉치 크기와 반비례
* 토큰
  * 언어를 다루는 가장 작은 기본 단위
  * word, morpheme, subword 타입
* 타입
  * 토큰의 대표 형태



> 한국어 예시

“이 사람은 내가 알던 사람이 아니다"

- 토큰화 :이 사람 은 내 가 알 더 ㄴ 사람 이 아니 다

- 표제어 추출 :이, 사람, 알다, 아니다 
- 품사 주석 :이/MM사람/NNG+은/JX나/NP+가/JKS알/VV+더/EP+ㄴ/ETM사람/NNG+이/JKS 아니/VA+다/EF 
- 토큰 수 :12개, 타입 수 :10개



> 영어 예시

“She is gone but she used to be mine" 

* 토큰화 : She is gone but she used to be mine 
* 표제어 추출 : She, be, go, but, use, to, mine 
* 품사 주석 : she_PRP is_VBZ gone_VBN but_IN she_PRP used_VBD to_TO be_VB mine_JJ 
* 토큰 수 : 9개, 타입 수 :8개



### N-gram

연속된 N개의 단위. 입력된 단위는 글자, 형태소, 단어, 어절 등으로 사용자가 지정할 수 있음. 

* 글자수 bi-gram 
  * 흔들리는 꽃들 속에서 네 샴푸향이 느껴진거야 : 흔+들, 들+리, 리+는, 는+꽃, 꽃+들 ...    
* 형태소 bi-gram
  * 흔들리는 꽃들 속에서 네 샴푸향이 느껴진거야 : 흔들리+는, 는+꽃, 꽃+들, 들+속, 속+에서 ...
* 어절 bi-gram
  * 흔들리는 꽃들 속에서 네 샴푸향이 느껴진거야 : 흔들리는+꽃들, 꽃들+속에서, 속에서+네 ...



### 표상 (Representation)

대표로 삼을 만큼 상징적인 것. 표상-하다 「001」 「동사」 【…을】 추상적이거나 드러나지 아니한 것을 구체적인 형상으로 드러내어 나타내다.



* 자연어처리 분야에서 표현으로 번역하기도 하나,자연어를 컴퓨터가 이해할 수 있는 기법으로 표시한다는 차원에서 표상이 더 적합. 

* 표시를 통해 재현 과정을 통해 나타내는 작업
* 사전학습모델(PLM, pretrained langage model), word2vec 등등

<br>

<br>

## 3. 자연어처리 데이터 형식

### HTML

![화면 캡처 2021-11-09 015517](https://user-images.githubusercontent.com/88299729/140785502-6828b0ae-5462-4c64-8e48-1248b5255791.png)

### XML

### ![화면 캡처 2021-11-09 015530](https://user-images.githubusercontent.com/88299729/140785533-335a03bb-bbe3-4eb9-acce-cbd16019eaaa.png)

### JSON

![화면 캡처 2021-11-09 015540](https://user-images.githubusercontent.com/88299729/140785556-1307310f-f4f0-4821-bad6-98f78b3b7e49.png)

### CSV, TSV

![화면 캡처 2021-11-09 015552](https://user-images.githubusercontent.com/88299729/140785572-56e37a82-9e5f-4c3d-b416-7d77a7c87b04.png)

<br>

<br>

## 4. 공개 데이터

### 경진대회 공개 데이터

* [DACON](https://dacon.io/)
* [Kaggle](https://www.kaggle.com/)



### 국가 주도 공공 데이터

* [모두의 말뭉치](https://corpus.korean.go.kr/)
* [AIHub](https://aihub.or.kr/)



### 오픈소스 + benchmark

* [Papers with Code](https://paperswithcode.com/)

* [NLP Progress](https://nlpprogress.com/)

  