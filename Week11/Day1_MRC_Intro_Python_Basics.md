## MRC Intro & Python Basics

### What is MRC?

사용자의 질문을 답할 수 있는 Question Answering 모델을 밑바닥부터 개발

![화면 캡처 2021-10-12 230643](https://user-images.githubusercontent.com/88299729/136982494-db034a4b-e941-4cc9-9168-6d74558f5515.png)

<br>

### Introduction to MRC

#### Machine Reading comprehension (MRC) 개념

기계 독해 (Machine Reading Comprehension)

![화면 캡처 2021-10-12 231023](https://user-images.githubusercontent.com/88299729/136982517-1a45f17e-23aa-4fe5-acd2-300805ce8da9.png)

* 주어진 지문(Context)를 이해하고, 주어진 질의(Query/Question)의 답변을 추론하는 문제

<br>

<br>

#### MRC의 종류

* Extractive Answer Datasets

  * 질의 (question)에 대한 답이 항상 주어진 지문(context)의 segment(or span)으로 존재

  ![화면 캡처 2021-10-12 231422](https://user-images.githubusercontent.com/88299729/136982568-a0cfc5ae-d0b4-4c78-a24a-a6bf48307bf4.png)

  ![화면 캡처 2021-10-12 231513](https://user-images.githubusercontent.com/88299729/136982623-d623b8ad-c82b-4ad7-94e3-e86d96684f52.png)

* Descriptive/Narrative Answer Datasets

  * 답이 지문 내에서 추출한 span이 아니라, 질의를 보고 생성된 sentence(or free-form)의 형태
  * e.g. MS MARCO, Narrative QA

  ![화면 캡처 2021-10-12 231814](https://user-images.githubusercontent.com/88299729/136982659-e5293c42-a618-4a37-a4c8-24398a5dc673.png)

* Multiple-choice Datasets

  * 질의에 대한 답을 여러 개의 answer candidates 중 하나로 고르는 형태

  * e.g. MC Test, RACE, ARC, etc

    ![화면 캡처 2021-10-12 231914](https://user-images.githubusercontent.com/88299729/136982708-e245fa84-5705-49ab-9158-bf34379d820f.png)

<br>

<br>

#### MRC Datasets

![화면 캡처 2021-10-12 232149](https://user-images.githubusercontent.com/88299729/136982806-c79dd708-96f7-4432-b829-2f5094b34c9a.png)

#### Challenges in MRC

* paraphrasing : 단어들의 구성이 유사하지는 않지만 동일한 의미의 문장을 이해

  ![화면 캡처 2021-10-12 233334](https://user-images.githubusercontent.com/88299729/136982831-d7bcb6b2-bbc3-4812-9965-9f823ec4d6ed.png)

  * Dataset example : DuoRC (paraphrased paragraph), QuoRef (coreference resolution: it, that과 같은 지칭하는 단어가 가르키는 단어를 찾을 수 있어야 함)



* unanswerable questions : 질문에 대한 답이 주어진 지문에 없더라도 답변을 할 수 있어야 한다.

  ![화면 캡처 2021-10-12 233551](https://user-images.githubusercontent.com/88299729/136982920-7fcc6763-74fa-40d1-b848-f95aceaea596.png)

  * Question with 'No Answer'
  * e.g. SQuAD 2.0



* Multi-hop reasoning : 여러개의 documents에서 질의에 대한 supporting fact를 찾아야지만 답을 찾을 수 있음

  ![화면 캡처 2021-10-12 234038](https://user-images.githubusercontent.com/88299729/136982960-1b651803-8667-4bd8-8f31-9ba6902e3090.png)

  * e.g. HotpotQA, QAngaroo

<br>

<br>

#### 평가 방법

* **Exact Match & F1 score** : extractive answer 와 multiple-choice answer datasets에 사용

  * Exact Match (EM or Accuracy) : 예측한 답과 ground-truth 가 정확히 일치하는 샘플의 비율

    * (The number of correct samples) / (The number of whole samples)

  * F1 score : 예측한 답과 ground-truth 사이의 token overlap을 F1으로 계산

    ![화면 캡처 2021-10-12 234747](https://user-images.githubusercontent.com/88299729/136983016-a177543c-5c10-470c-9f1d-708a35f4f2dd.png)

    <br>

    

* **ROUGE-L score & BLEU** : descriptive answer datasets에 사용 => Ground-truth와 예측한 답 사이의 overlap을 계산

  * ROUGE-L score : 예측한 값과 ground-truth 사이의 overlap recall
    * ROUGE-**L**의 **L**은 LCS(Longest common subsequence)를 기반이라는 의미

  * BLEU(Bilingual Evaluation Understudy) : 예측한 답과 ground-truth 사이의 precision
    * (BLEU-**n**의 n은 uniform n-gram weight를 의미)

<br>

<br>

### Unicode & Tokenization

#### Unicode란?

![화면 캡처 2021-10-12 235436](https://user-images.githubusercontent.com/88299729/136983066-6146659e-8847-48e9-bdb0-d624b87115a5.png)

전 세계의 모든 문자를 일관되게 표현하고 다룰 수 있도록 만들어진 문자셋 각 문자마다 숫자 하나에 매핑한다.

<br>

#### 인코딩 & UTF-8

* **인코딩이란?**

  ![화면 캡처 2021-10-12 235824](https://user-images.githubusercontent.com/88299729/136983098-e88bb8d5-2d59-4bf6-88c1-d5cbe63fe865.png)

  문자를 컴퓨터에서 저장 및 처리 할 수 있게 이진수로 바꾸는 것

* **UTF-8 (Unicode Transformation Format)**

  * UTF-8는 현재 가장 많이 쓰는 인코딩 방식
  * 문자 타입에 따라 다른 길이의 바이트를 할당
    * 1byte : Standard ASCII 
    * 2bytes : Arabic, Hebrew, most European scripts
    * 3bytes : BMP(Basic Multilingual Plane)- 대부분의 현대 글자 (한글 포함)
    * 4bytes : All Unicode characters- 이모지 등



#### Python에서 Unicode 다루기

Python3부터 string타입은 유니코드 표준을 사용

![화면 캡처 2021-10-13 000111](https://user-images.githubusercontent.com/88299729/136983187-d1ae50cb-80f2-4038-b9c4-4037abb8c183.png)

* ord 
  * 문자를 유니코드 code point로 변환 

* chr
  * Code point를 문자로 변환



#### Unicode와 한국어

한국어는 한자 다음으로 유니코드에서 많은 코드를 차지하고 있는 문자

* 완성형
  * 현대 한국어의 자모 조합으로 나타낼 수 있는 모든 완성형 한글 11,172자(가,각,…, , )
  * (U+AC00~U+D7A3)
* 조합형
  * 조합하여 글자를 만들 수 있는 초·중·종성 
  * (U+1100~U+11FF,U+A960~U+A97F,U+D7B0~U+D7FF)



#### Tokenizing

* 텍스트를 토큰 단위로 나누는 것 
* 단어(띄어쓰기 기준), 형태소, subword 등 여러 토큰 기준이 사용된다.



#### Subword Tokenizing

* 자주 쓰이는 글자 조합은 한 단위로 취급하고,자주 쓰이지 않는 조합은 subword로 쪼갠다
* "##"은 디코딩 (토크나이징의 반대 과정)을 할 때 해당 토큰을 앞 토큰에 띄어쓰기 없이 붙인다는 것을 뜻한다.

![화면 캡처 2021-10-13 000515](https://user-images.githubusercontent.com/88299729/136983221-18f17960-0b4a-4af5-a11b-49f680e4b23d.png)



#### BPE (Byte-Pair Encoding)

* 데이터 압축용으로 제안된 알고리즘. 
* NLP에서 토크나이징용으로 활발하게 사용되고 있다.



![화면 캡처 2021-10-13 000749](https://user-images.githubusercontent.com/88299729/136983296-95136a83-ac35-4cae-a8dd-08cad0b1d24e.png)

1. 가장 자주 나오는 글자 단위 Bigram (or Byte pair) 를 다른 글자로 치환
2. 치환된 글자를 저장 
3. 1~2번을 반복

### Looking into the Dataset

![화면 캡처 2021-10-13 000830](https://user-images.githubusercontent.com/88299729/136983389-6430f00d-9771-4dec-9473-fc0c9b7eccf0.png)

#### KorQuAD 훑어보기

* LGCNS가 AI언어지능 연구를 위해 공개한 질의응답/기계독해 한국어 데이터셋 
* 인공지능이 한국어 질문에 대한 답변을 하도록 필요한 학습 데이터셋



#### KorQuAD란?

![화면 캡처 2021-10-13 001009](https://user-images.githubusercontent.com/88299729/136983421-7c7d4cfe-b46f-4065-8a98-3a3ec541513f.png)

LG CNS가 AI 언어지능 연구를 위해 공개한 질의응답/기계독해 한국어 데이터셋 

* 인공지능이 한국어 질문에 대한 답변을 하도록 필요한 학습 데이터셋 
* 1,550개의 위키피디아 문서에 대해서 10,649건의 하위 문서들과 크라우드 소싱을 통해 제작한 63,952 개의 질의응답 쌍으로 구성되어 있음 (TRAIN60,407/DEV5,774/TEST3,898) 
* 누구나 데이터를 내려받고, 학습한 모델을 제출하고 공개된 리더보드에 평가를 받을 수 있음 -> 객관적인 기준을 가진 연구 결과 공유가 가능해짐 
* 현재 v1.0,v2.0공개:2.0은 보다 긴 분량의 문서가 포함되어 있으며,단순 자연어 문장 뿐 아니라 복잡한 표와 리스트 등을 포함하는 HTML 형태로 표현되어 있어 문서 전체 구조에 대한 이해가 필요

