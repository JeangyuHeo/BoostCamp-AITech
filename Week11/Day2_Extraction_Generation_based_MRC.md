## Extraction-based MRC

### Extraction-based MRC

#### 정의

![화면 캡처 2021-10-13 153926](https://user-images.githubusercontent.com/88299729/137131489-35c527ac-7fb1-49b1-819f-747b08dc7407.png)

* 질문(question)의 답변(answer)이 항상 주어진 지문(context)내에 span으로 존재 

* e.g. SQuAD, KorQuAD, NewsQA, Natural Questions, etc
  * Extraction-based MRC datasets in HuggingFace datasets (https://huggingface.co/datasets)

#### 평가 방법

* **Exact Match (EM)**
  * Score 예측 값과 정답이 캐릭터 단위로 완전히 똑같을 경우에만 1점 부여. 하나라도 다른 경우 0점.
* **F1 Score**
  * 예측값과 정답의 overlap을 비율로 계산. 
  * 0점과 1점사이의 부분점수를 받을 수 있음.

<img src="https://user-images.githubusercontent.com/88299729/137131552-6a0c43f7-1c30-4eb1-a45f-c3446f7da1bb.png" alt="화면 캡처 2021-10-13 154424" style="zoom:80%;" /><img src="https://user-images.githubusercontent.com/88299729/137131518-59f1b181-ec76-43b5-92b9-f0b386e66702.png" alt="화면 캡처 2021-10-13 154411" style="zoom:80%;" />

#### Overview

![화면 캡처 2021-10-13 154443](https://user-images.githubusercontent.com/88299729/137131583-34577faf-e965-4814-95d5-392cd5fd9aa2.png)

### Pre-processing

#### Tokenization

텍스트를 작은 단위 (Token) 로 나누는 것 

* 띄어쓰기 기준, 형태소, subword 등 여러 단위 토큰 기준이 사용됨 

* 최근엔 Out-Of-Vocabulary (OOV) 문제를 해결해주고 정보학적으로 이점을 가진 Byte Pair Encoding (BPE)을 주로 사용함 

* 본강에선 BPE방법론중 하나인 WordPiece Tokenizer를 사용

  ![화면 캡처 2021-10-13 155855](https://user-images.githubusercontent.com/88299729/137131795-2152df3b-2591-48f9-80ac-d49b7ebd63a0.png)

#### special Tokens

![화면 캡처 2021-10-13 211750](https://user-images.githubusercontent.com/88299729/137131850-f861880b-0086-4f51-968d-3294021447c7.png)

#### Attention Mask

![화면 캡처 2021-10-13 211831](https://user-images.githubusercontent.com/88299729/137131885-b7e31822-088a-4ce6-b689-6e7f50d22b7f.png)

* 입력 시퀸스 중에서 attention을 연산할 때 무시할 토큰을 표시 
* 0은 무시, 1은 연산에 포함 
* 보통 [PAD]와 같은 의미가 없는 특수토큰을 무시하기 위해 사용

#### Token Type IDs

![화면 캡처 2021-10-13 211909](https://user-images.githubusercontent.com/88299729/137131922-fe201baf-fa34-48ff-be78-258d949368ca.png)

* 입력이 2개이상의 시퀸스일 때 (예: 질문 & 지문), 각각에게 ID를 부여하여 모델이 구분해서 해석하도록 유도

#### 모델 출력 값

* 정답은 문서내 존재하는 연속된 단어토큰 (span)이므로, span의 시작과 끝 위치를 알면 정답을 맞출 수 있음
* Extraction-based에선 답안을 생성하기 보다, 시작위치와 끝위치를 예측하도록 학습함. 즉, Token Classification문제로 치환

![화면 캡처 2021-10-13 212010](https://user-images.githubusercontent.com/88299729/137131954-299a1e43-6a9d-4f1a-bb3c-5b6ab82df3dd.png)

### Fine-tuning

![화면 캡처 2021-10-13 212033](https://user-images.githubusercontent.com/88299729/137132012-e871b5c5-1d04-4c4f-a2e8-c46ed647a85f.png)

### Post-processing

#### 불가능한 답 제거하기

다음과 같은 경우 candidate list에서 제거 

* End position이 start position보다 앞에 있는 경우 (e.g. start=90,end=80) 
* 예측한 위치가 context를 벗어난 경우 (e.g. question 위치쪽에 답이 나온 경우) 
* 미리 설정한 max_answer_length 보다 길이가 더 긴 경우

#### 최적의 답안 찾기

1. Start / end position prediction에서 score(logits)가 가장 높은 N개를 각각 찾는다. 
2. 불가능한 start/end조합을 제거한다. 
3. 가능한 조합들을 score의 합이 큰 순서대로 정렬한다. 
4. Score가 가장 큰 조합을 최종 예측으로 선정한다. 
5. Top-k가 필요한 경우 차례대로 내보낸다.



## Generation-based MRC

### Generation-based MRC

#### Generation-based MRC 개념 및 개요

* **MRC 문제를 푸는 방법**

  * Extraction-based MRC : 지문 (context) 내 답의 위치를 예측 => 분류 문제 (classification)

  ![화면 캡처 2021-10-14 141250](https://user-images.githubusercontent.com/88299729/137261414-1150f0a5-6756-44a0-9f36-896c7daecf58.png)

  * Generation-based MRC : 주어진 지문과 질의 (question)를 보고, 답변을 생성 => 생성 문제 (generation)

![화면 캡처 2021-10-14 141255](https://user-images.githubusercontent.com/88299729/137261448-d5e898c2-e3e1-4a7d-9826-1762db9121bf.png)





#### Generation-based MRC 평가 방법

동일한 extractive answer datasets => Extraction-based MRC와 동일한 평가 방법을 사용 (recap)

* **Exact Match (EM) Score**
  * EM = 1 if (Characters of the prediction) == (Characters of ground-truth) else 0
* **F1 Score**
  * 예측한 답과 ground-truth 사이의 token overlap을 F1으로 계산

![image-20211014141921831](https://user-images.githubusercontent.com/88299729/137261514-18a75376-2bfc-4fc5-83c4-69ea3854fd77.png)



#### Generation-based MRC Overview

![화면 캡처 2021-10-14 142040](https://user-images.githubusercontent.com/88299729/137261537-e8cc4fcc-acef-471f-b2cb-21b6dbc1ea02.png)

#### Generation-based MRC & Extraction-based MRC 비교

![화면 캡처 2021-10-14 142733](https://user-images.githubusercontent.com/88299729/137261557-4eee7704-e65f-4e01-9e97-db6c50706672.png)

* **MRC 모델 구조**
  * Seq-to-seq PLM 구조 (generation) vs. PLM + Classifier구조 (extraction)
* **Loss 계산을 위한 답의 형태 / Prediction의 형태**
  * Free-form text 형태 (generation) vs. 지문 내 답의 위치 (extraction)
  * => Extraction-based MRC : F1 계산을 위해 text로의 별도 변환 과정이 필요

### Pre-processing

#### 입력 표현 - 데이터 예시

![화면 캡처 2021-10-14 143326](https://user-images.githubusercontent.com/88299729/137261625-0f17a868-e010-4a86-b522-21dde639b06a.png)

#### 입력 표현 - 토큰화

Tokenization (토큰화) : 텍스트를 의미를 가진 작은 단위로 나눈 것 (형태소)

* Extration-based MRC와 같이 WordPiece Tokenizer를 사용함
  * WordPiece Tokenizer 사전 학습 단계에서 먼저 학습에 사용한 전체 데이터 집합 (Corpus)에 대해서 구축되어 있어야함
  * 구축 과정에서 미리 각 단어 토큰들에 대해 순서대로 번호(index)를 부여해둠
* Tokenizer은 입력 텍스트를 토큰화 한 뒤, 각 토큰을 미리 만들어둔 단어 사전에 따라 인덱스로 변환

![화면 캡처 2021-10-14 143825](https://user-images.githubusercontent.com/88299729/137261645-63c5d436-7af2-49ef-81c3-0b44b31e8129.png)



#### 입력 표현 - Special Token

* 학습 시에만 사용되며 단어 자체의 의미는 가지지 않는 특별한 토큰
  * SOS(Start Of Sentence), EOS(End Of Sentence), CLS, SEP, PAD, UNK.. etc
* => Extraction-based MRC에선 CLS, SEP, PAD 토큰을 사용
* => Generation-based MRC 에서도 PAD 토큰은 사용됨, CLS, SEP 토큰 또한 사용할 수 있으나, 대신 자연어를 이용하여 정해진 텍스트 포맷(format)으로 데이터를 생성

![화면 캡처 2021-10-14 144521](https://user-images.githubusercontent.com/88299729/137261676-f27a3924-818e-4246-a96b-8c43a7003383.png)



#### 입력 표현 - additional information

* **Attention mask**
  * Extraction-based MRC와 똑같이 attention 연산을 수행할 지 결정하는 attention mask 존재
* **Token type ids**
  * BERT와 달리 BART에서는 입력시퀀스에 대한 구분이 없어 token_type_ids가 존재하지 않음
  * 따라서, Extraction-based MRC와 달리 입력에 token_type_ids 가 들어가지 않음

![화면 캡처 2021-10-14 144759](https://user-images.githubusercontent.com/88299729/137261701-6ec9c29e-1548-4894-a105-b71a90762cf8.png)

#### 출력 표현 - 정답 출력

* **Sequence of token ids**
  * Extraction-based MRC에선 텍스트를 생성해내는 대신 시작/끝 토큰의 위치를 출력하는 것이 모델의 최종 목표였음
  * Generation-based MRC는 그보다 조금 더 어려운 실제 텍스트를 생성하는 과제를 수행
  * 전체 sequence의 각 위치 마다 모델이 아는 모든 단어들 중 하나의 단어를 맞추는 classification 문제

![화면 캡처 2021-10-14 145610](https://user-images.githubusercontent.com/88299729/137261719-4ed5b18d-f9f5-4a1d-84c0-2fe15a904f2e.png)

### Model

#### BART

![화면 캡처 2021-10-14 145632](https://user-images.githubusercontent.com/88299729/137261740-7ca542c2-44e0-4bca-bf4b-fe67ec5be3b3.png)

기계 독해, 기계 번역, 요약, 대화 등 sequence to sequence 문제의 pre-training을 위한 denoising autoencoder



#### BART Encoder & Decoder

![화면 캡처 2021-10-14 145812](https://user-images.githubusercontent.com/88299729/137261803-d8e97c6a-cce0-46ac-af26-7a226e09445c.png)

* BART의 인코더는 BERT처럼 bi-directional
* BART의 디코더는 GPT처럼 uni-directional (auto regressive)

![화면 캡처 2021-10-14 150258](https://user-images.githubusercontent.com/88299729/137261840-18cdbf25-a819-4560-af4f-76ef297d77aa.png)

#### Pre-training BART

![화면 캡처 2021-10-14 150408](https://user-images.githubusercontent.com/88299729/137261863-34d9f775-bc19-4731-a741-2aa3b2ed595d.png)

* BART는 텍스트에 노이즈를 주고 원래 텍스트를 복구하는 문제를 푸는 것으로 pre-training 함



### Post-processing

#### Decoding

![화면 캡처 2021-10-14 150720](https://user-images.githubusercontent.com/88299729/137261905-af330149-0f38-44b1-bc83-01205484cfa6.png)

* 디코더에서 이전 스텝에서 나온 출력이 다음 스텝의 입력으로 들어감 (autoregressive)
* 맨 처음 입력은 문장 시작을 뜻하는 special token



#### Searching

![화면 캡처 2021-10-14 150757](https://user-images.githubusercontent.com/88299729/137261929-a1b111c9-1792-4aec-9e9d-f4915ac7c1a2.png)

