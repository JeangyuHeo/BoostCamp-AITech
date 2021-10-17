## Passage Retrieval - Dense Embedding

<br>

### Introduction to Dense Embedding

<br>

#### Passage Embedding

<img width="391" alt="Screen Shot 2021-10-17 at 5 14 36 PM" src="https://user-images.githubusercontent.com/88299729/137619257-ea207a59-f1c4-4bf8-b400-2cc96849a08b.png">

구절(Passage)을 벡터로 변환하는 것

<br>

#### Sparse Embedding

<img width="479" alt="Screen Shot 2021-10-17 at 5 16 17 PM" src="https://user-images.githubusercontent.com/88299729/137619277-6b9585fb-6b37-49e3-aad0-328c44d34aed.png">

TF-IDF 벡터는 Sparse 하다.

<br>

#### Limitation of sparse embedding

<img width="509" alt="Screen Shot 2021-10-17 at 5 17 35 PM" src="https://user-images.githubusercontent.com/88299729/137619311-5943cf02-5898-48a6-b6be-9af57a9a9a36.png">

1. 차원의 수가 매우 크다 => compressed format으로 극복 가능
2. 유사성을 고려하지 못한다

<br>

#### What is Dense Embedding?

<img width="551" alt="Screen Shot 2021-10-17 at 5 23 27 PM" src="https://user-images.githubusercontent.com/88299729/137619346-882fc788-1746-49b3-ac73-84fa0b6c5848.png">

Complementary to sparse representations by design

* 더 작은 차원의 고밀도 벡터 (length = 50-1000)
* 각 차원이 특정 term에 대응되지 않음
* 대부분의 요소가 non-zero 값

<br>

#### Retrieval : Sparse vs Dense

<img width="451" alt="Screen Shot 2021-10-17 at 5 25 16 PM" src="https://user-images.githubusercontent.com/88299729/137619401-56918b7e-966d-4b07-94f3-f003f259a54f.png">

<img width="462" alt="Screen Shot 2021-10-17 at 5 25 52 PM" src="https://user-images.githubusercontent.com/88299729/137619412-2a1e77a8-73a0-421b-80ed-15753ef04327.png">

<br>

#### Overview of Passage Retrieval with Dense Embedding

<img width="438" alt="Screen Shot 2021-10-17 at 5 26 40 PM" src="https://user-images.githubusercontent.com/88299729/137619430-4f6c9629-8892-40b1-938f-cda78f4b630f.png">

<img width="487" alt="Screen Shot 2021-10-17 at 5 26 55 PM" src="https://user-images.githubusercontent.com/88299729/137619441-3df21436-c501-4a1e-8a59-661b9df4b9b3.png">

<br>

### Training Dense Encoder

<br>

#### What can be Dense Encoder?



* BERT와 같은 Pre-trained language model (PLM)이 자주 사용

* 그 외 다양한 neural network 구조도 가능

* BERT as dense encoder => [CLS] token 의 output 사용

<br>

#### Dense Encoder 구조

<img width="477" alt="Screen Shot 2021-10-17 at 5 29 53 PM" src="https://user-images.githubusercontent.com/88299729/137619463-50a4d4c8-cb1e-46d1-a940-692f671c2a06.png">

<br>

#### Dense Encoder 학습 목표와 학습 데이터

<img width="500" alt="Screen Shot 2021-10-17 at 5 34 52 PM" src="https://user-images.githubusercontent.com/88299729/137619476-28877e53-d8c6-4a53-8540-59e946f8a5a7.png">

**학습목표**

* 연관된 question과 passage dense embedding 간의 거리를 좁히는 것 (또는 inner product를 높이는 것). 즉 **higher similarity**.

**Challenge**

* 연관된 question / passage를 어떻게 찾을 것인가? => 기존 MRC 데이터셋을 활용

<br>

#### Dense Encoder 학습 목표와 학습 데이터 - Negative Sampling

1. 연관된 question과 passage 간의 dense embedding 거리를 좁히는 것 (higher similarity) => Positive
2. 연관되지 않은 question과 passage 간의 embedding 거리는 멀어야 함 => Negative

<img width="249" alt="Screen Shot 2021-10-17 at 5 37 10 PM" src="https://user-images.githubusercontent.com/88299729/137619513-68840362-de11-4b52-bbdf-d6924226b4b5.png">

> Choosing negative examples:

1. Corpus 내에서 랜덤하게 뽑기
2. 좀 더 헷갈리는 negative 샘플들 뽑기 (e.g. 높은 TF-IDF 스코어를 가지지만 답을 포함하지 않는 샘플)

<br>

#### Objective function

<img width="458" alt="Screen Shot 2021-10-17 at 5 39 28 PM" src="https://user-images.githubusercontent.com/88299729/137619540-87a84284-c5d7-4016-b93c-c684784130cf.png">

Positive passage 에 대한 negative log liklihood (NLL) loss 사용

<br>

#### Evaluation Metric for Dense Encoder

**Top-k retrieval accuracy** 

<img width="242" alt="Screen Shot 2021-10-17 at 5 40 54 PM" src="https://user-images.githubusercontent.com/88299729/137619549-21ca09cc-bb82-4932-817c-6b28ccd8f930.png">

* retrieve 된 passage 중에 답을 포함하는 passage의 비율

<br>

### Passage Retrieval with Dense Encoder

<br>

#### From dense encoding to retrieval

<img width="402" alt="Screen Shot 2021-10-17 at 5 42 15 PM" src="https://user-images.githubusercontent.com/88299729/137619556-90dcc57d-cd3f-4771-a9a4-b1228a066f87.png">

**Inference**

* Passage와 query를 각각 embedding한 후, query로부터 가까운 순서대로 passage의 순위를 매김

<br>

#### From retrieval to open-domain question answering

<img width="467" alt="Screen Shot 2021-10-17 at 5 42 55 PM" src="https://user-images.githubusercontent.com/88299729/137619570-048e2d02-8424-4219-bcaf-6c8f8f9f0e91.png">

Retriever를 통해 찾아낸 Passage을 활용, MRC (Machine Reading Comprehension) 모델로 답을 찾음.

<br>

#### How to make better dense encoding

* 학습 방법 개선 (e.g. DPR)
* 인코더 모델 개선 (BERT보다 큰, 정확한 Pretrained 모델)
* 데이터 개선 (더 많은 데이터, 전처리, 등)