## MRC Intro & Python Basics

### What is MRC?

사용자의 질문을 답할 수 있는 Question Answering 모델을 밑바닥부터 개발



### Introduction to MRC

#### Machine Reading comprehension (MRC) 개념

기계 독해 (Machine Reading Comprehension)

* 주어진 지문(Context)를 이해하고, 주어진 질의(Query/Question)의 답변을 추론하는 문제



#### MRC의 종류

* Extractive Answer Datasets
  * 질의 (question)에 대한 답이 항상 주어진 지문(context)의 segment(or span)으로 존재
* Descriptive/Narrative Answer Datasets
  * 답이 지문 내에서 추출한 span이 아니라, 질의를 보고 생성된 sentence(or free-form)의 형태
  * e.g. MS MARCO, Narrative QA
* Multiple-choice Datasets
  * 질의에 대한 답을 여러 개의 answer candidates 중 하나로 고르는 형태
  * e.g. MC Test, RACE, ARC, etc



#### MRC Datasets



#### Challenges in MRC

* 단어들의 구성이 유사하지는 않지만 동일한 의미의 문장을 이해
  * Dataset example : DuoRC (paraphrased paragraph), QuoRef (coreference resolution: it, that과 같은 지칭하는 단어가 가르키는 단어를 찾을 수 있어야 함)



* unanswerable questions : 답변이 지문에 없더라도 답변을 할 수 있어야 한다.
  * Question with 'No Answer'
  * e.g. SQuAD 2.0



* Multi-hop reasoning : 여러개의 documents에서 질의에 대한 supporting fact를 찾아야지만 답을 찾을 수 있음



### Unicode & Tokenization



### Looking into the Dataset

