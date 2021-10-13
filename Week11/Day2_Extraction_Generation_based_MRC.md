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

