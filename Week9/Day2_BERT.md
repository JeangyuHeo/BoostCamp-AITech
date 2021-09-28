## BERT 언어모델

**BERT모델을 소개합니다.**

### BERT 모델 소개

* Transformer의 Self-Attention 구조를 사용하였고, Encoder부분만을 가지고 제작되었다.
* Data를 부분적으로 Masking하고 그 부분을 맞추는 방식으로 학습이 진행된다.



![image-20210929015701023](https://user-images.githubusercontent.com/88299729/135138849-5212f7e7-4987-41e3-a591-daa1593ec178.png)



#### 모델 구조도

![image-20210929020413223](https://user-images.githubusercontent.com/88299729/135138902-74a31a28-3696-40f5-936a-3ec44e3afa0c.png)

#### 학습 코퍼스 데이터 

* BooksCorpus (800Mwords) 
* EnglishWikipedia(2,500Mwordswithoutlists,tablesandheaders) 
* 30,000tokenvocabulary



#### 데이터의 tokenizing 

* WordPiece tokenizing 
* He likes playing -> He likes play ##ing 
* 입력 문장을 tokenizing하고,그 token들로 ‘tokensequence’를 만들어 학습에 사용 
* 2개의 tokensequence가 학습에 사용

![image-20210929023723052](https://user-images.githubusercontent.com/88299729/135138924-f93adc39-ebd6-448f-89d4-6eb1fb65a506.png)



#### BERT - Masked Language Model

![image-20210929023800411](https://user-images.githubusercontent.com/88299729/135138955-eef9a4e1-c481-4b51-8a52-76ed104d6679.png)

* 80% 확률로 데이터를 Mask 해주고, 10% 확률로 랜덤하게 값을 바꿔주고, 10% 확률로 바꿔주지 않는다.

#### GPT-1 vs BERT vs GPT-2

![image-20210929020020957](https://user-images.githubusercontent.com/88299729/135138997-f375fde7-4a63-4958-88a5-40775395978e.png)



### BERT의 응용

#### BERT를 이용한 TASK

![image-20210929024007474](https://user-images.githubusercontent.com/88299729/135139035-8ee9c875-f931-4cda-a195-4b5782159bda.png)



* 단일 문장 분류
  * 감정 분석
  * 관계 추출
* 두 문장 관계 분류
  * 의미 비교
* 문장 토큰 분류
  * 개체명 분석
* 기계 독해 정답 분류
  * 기계 독해

### 한국어 BERT 모델

#### ETRI KoBERT

![image-20210929024524891](https://user-images.githubusercontent.com/88299729/135139132-f3b0b640-2c09-455d-a12a-774f10460e2a.png)



#### Advanced BERT model

![image-20210929024424558](https://user-images.githubusercontent.com/88299729/135139098-e65fa79a-7c5c-4e63-8b30-691e1c31a63a.png)

* KBQA에서 가장 중요한 entity정보가 기존 BERT에서는 무시
* Entitylinking을 통한 주요 entity추출 및 entitytag부착
* Entityembeddinglayer의 추가
* 형태소 분석을 통해 NNP와 entity우선 chunkingmasking

![image-20210929024403875](https://user-images.githubusercontent.com/88299729/135139061-66601481-99ce-49e7-90b8-104dad12d663.png)