## Passage Retrieval - Sparse Embedding



### Introduction to Passage Retrieval

<br>

#### Passage Retrieval

<img width="359" alt="Screen Shot 2021-10-17 at 4 07 42 PM" src="https://user-images.githubusercontent.com/88299729/137617448-cda36f89-0523-4111-977b-1e2e72504255.png" style="zoom:80%;" ><img width="443" alt="Screen Shot 2021-10-17 at 4 08 00 PM" src="https://user-images.githubusercontent.com/88299729/137617475-dbcdcd51-3b24-47c9-90c4-9cb4867429e1.png" style="zoom:80%;" >

질문(query)에 맞는 문서(passage)를 찾는 것

<br>

#### Passage Retrieval with MRC

<img width="411" alt="Screen Shot 2021-10-17 at 4 11 51 PM" src="https://user-images.githubusercontent.com/88299729/137617494-5cbcdf2c-e727-4492-b2ba-a97c617a4cfc.png">

**Open-domain Question Answering**: 대규모의 문서 중에서 질문에 대한 답을 찾기

*  Passage Retrieval과 MRC를 이어서 2-Stage로 만들 수 있음.

<br>

#### Overview of Passage Retrieval

<img width="526" alt="Screen Shot 2021-10-17 at 4 13 59 PM" src="https://user-images.githubusercontent.com/88299729/137617507-31529284-ef11-4a12-9d5c-e12e4a0106cd.png">

Query와 Passage 임베딩 한 뒤 유사도로 랭킹을 매기고, 유사도가 가장 높은 Passage를 선택

<br>

### Passage Embedding and Sparse Embedding

#### Passage Embedding Space

<img width="436" alt="Screen Shot 2021-10-17 at 4 17 18 PM" src="https://user-images.githubusercontent.com/88299729/137617523-1547753b-91d0-437f-8105-87e7192abd0e.png">

* Passage Embedding의 벡터 공간
* 벡터화된 Passage를 이용하여 Passage 간 유사도 등을 알고리즘으로 계산 할 수 있음.

<br>

#### Sparse Embedding 소개

1. BoW를 구성하는 방법 => n-gram

   <img width="517" alt="Screen Shot 2021-10-17 at 4 18 53 PM" src="https://user-images.githubusercontent.com/88299729/137617537-836a2bad-364c-4fb6-9b5f-3779181eb43b.png">

   - unigram (1-gram): It was the best of times => It, was, the, best, of, times
   - bigram (2-gram): It was the best of times => It was, was the, the best, best of, of times

2. Term value를 결정하는 방법

   <img width="524" alt="Screen Shot 2021-10-17 at 4 22 57 PM" src="https://user-images.githubusercontent.com/88299729/137617555-35e3fa6c-df24-4b91-9156-31ead7fb13e4.png">

   -  Term이 document에 등장하는지 (binary)
   - Term이 몇번 등장하는지 (term frequency), 등 (e.g. TF-IDF)

<br>

#### Sparse Embedding 특징

1. **Dimension of embedding vector = number of terms**

   <img width="402" alt="Screen Shot 2021-10-17 at 4 24 43 PM" src="https://user-images.githubusercontent.com/88299729/137617571-13ba0eb9-ff2d-4b9a-bc06-f1fe4b167cf8.png">

   - 등장하는 단어가 많아질수록 증가
   - N-gram의 n이 커질수록 증가

2. Term overlap을 정확하게 잡아내야 할 때 유용

   <img width="360" alt="Screen Shot 2021-10-17 at 4 25 52 PM" src="https://user-images.githubusercontent.com/88299729/137617596-4f37e5c1-0074-4617-aa7f-f0f0e38c0152.png">

3. 반면, 의미(semantic)가 비슷하지만 다른 단어인 경우 비교가 불가



<br>

### TF-IDF (Term Frequency - Inverse Document Frequency)

<br>

#### TF-IDF 소개

* Term Frequency (TF) : 단어의 등장 빈도

  <img width="411" alt="Screen Shot 2021-10-17 at 4 32 38 PM" src="https://user-images.githubusercontent.com/88299729/137617605-03219b99-7198-44c1-931d-1cd63e3e5430.png">

* Inverse Document Frequency (IDF) : 단어가 제공하는 정보의 양

<img width="271" alt="Screen Shot 2021-10-17 at 4 34 00 PM" src="https://user-images.githubusercontent.com/88299729/137617679-03fa70e4-5ecf-4e47-83d8-71fbc408b910.png"><img width="293" alt="Screen Shot 2021-10-17 at 4 34 29 PM" src="https://user-images.githubusercontent.com/88299729/137617685-58b06be1-5f36-47f8-a968-e689ed3cab03.png">

<br>

E.g. It was the best of times

=> It, was, the, of : 자주 등장하지만 제공하는 정보량이 적음

=> best, times: 좀 더 많은 정보를 제공

<br>

#### Term Frequency (TF)

해당 문서 내 단어의 등장 빈도

1. Raw count
2. Adjusted for doc length : raw count / num words (TF)
3. Other variants : binary, log normalization, etc.

<br>

#### Inverse Document Frequency (IDF)

단어가 제공하는 정보의 양

<br>

#### Combine TF & IDF

TF-IDF(t, d): TF-IDF for term t in document d,

<img width="137" alt="Screen Shot 2021-10-17 at 4 36 07 PM" src="https://user-images.githubusercontent.com/88299729/137617695-31444ab5-ff4c-4c61-bdc1-95e06c1d9921.png">

1) ‘a’, ‘the’ 등관사⇒ Low TF-IDF
   * TF는 높을 수 있지만, IDF가 0 에 가까울 것
   * 거의 모든 document에 등장 ⇒ N ≈ DF(t) ⇒ log(N/DF) ≈ 0
2) 자주 등장하지 않는 고유명사 (ex. 사람 이름, 지명 등) ⇒ High TF-IDF
   * IDF가 커지면서 전체적인 TF-IDF 값이 증가

<br>

#### TF-IDF 계산하기

* **실험 할 데이터**

<img width="292" alt="Screen Shot 2021-10-17 at 4 38 55 PM" src="https://user-images.githubusercontent.com/88299729/137617754-b3fb4b86-ca3d-462f-a5a6-4b5e41f77638.png">

* **토크나이저**

<img width="380" alt="Screen Shot 2021-10-17 at 4 39 14 PM" src="https://user-images.githubusercontent.com/88299729/137617761-e3664da2-f311-48a6-a7fa-05a502181274.png">

* **Term Frequency (TF) : 단어의 등장 빈도**
  * TF (t,d) : TF for term t and document d

<img width="561" alt="Screen Shot 2021-10-17 at 4 40 38 PM" src="https://user-images.githubusercontent.com/88299729/137617767-a222957d-bc42-45b8-995a-be2e53811e60.png">

* **Inverse Document Frequency (IDF) : 단어가 제공하는 정보의 양**

<img width="570" alt="Screen Shot 2021-10-17 at 4 41 16 PM" src="https://user-images.githubusercontent.com/88299729/137617774-b2394e30-3e3f-443f-84e4-3bec5af59413.png">

* **TF-IDF 계산**

<img width="563" alt="Screen Shot 2021-10-17 at 4 42 56 PM" src="https://user-images.githubusercontent.com/88299729/137617787-da41233f-c0ce-4719-8da6-346b2747b12c.png">

<br>

#### TF-IDF를 이용해 유사도 구해보기

* 목표 : 계산한 문서 TF-IDF를 가지고 질의 TF-IDF를 계산한 후 가장 관련 있는 문서를 찾기
* 질문 : 주연은 BTS의 누구를 가장 잘 생겼다고 생각한다 ?

<img width="514" alt="Screen Shot 2021-10-17 at 4 44 04 PM" src="https://user-images.githubusercontent.com/88299729/137617867-96d86d30-00c4-4abf-95e8-b46cdae9e8e4.png">

**목표: 계산한 TF-IDF를 가지고 사용자가 물어본 질의에 대해 가장 관련있는 문서를 찾자**

1. 사용자가 입력한 질의를 토큰화

2. 기존에 단어 사전에 없는 토큰들은 제외

3. 질의를 하나의 문서로 생각하고, 이에 대한 TF-IDF 계산

4. 질의 TF-IDF 값과 각 문서별 TF-IDF 값을 곱하여 유사도 점수 계산

   <img width="407" alt="Screen Shot 2021-10-17 at 4 45 28 PM" src="https://user-images.githubusercontent.com/88299729/137617874-26a3e7e3-0cc9-4a1d-9603-b6d308287921.png">

5. 가장 높은 점수를 가지는 문서 선택



#### BM25 란?

TF-IDF 의 개념을 바탕으로, 문서의 길이까지 고려하여 점수를 매김

* TF 값에 한계를 지정해두어 일정한 범위를 유지하도록 함

* 평균적인 문서의 길이 보다 더 작은 문서에서 단어가 매칭된 경우 그 문서에 대해 가중치를 부여

* 실제 검색엔진, 추천 시스템 등에서 아직까지도 많이 사용되는 알고리즘

<img width="554" alt="Screen Shot 2021-10-17 at 4 50 45 PM" src="https://user-images.githubusercontent.com/88299729/137617882-30bf9a6a-0fd8-420e-a507-99a55c5145ea.png">

