## Transformers 와 multi-modal 연구

### BERT 이후의 다양한 LM

BERT 이후에 등장한 다양한 언어 모델을 소개합니다.

<img width="639" alt="Screen Shot 2021-10-10 at 5 59 07 PM" src="https://user-images.githubusercontent.com/88299729/136694887-32013896-b6e0-419e-b556-bcfe78723093.png">

#### XLNET

* **Relative positional encoding 방식 적용 (Transformer-XL)**

  <img width="286" alt="Screen Shot 2021-10-10 at 6 02 50 PM" src="https://user-images.githubusercontent.com/88299729/136694919-34f66f35-0ff4-4811-9a06-3132e581410d.png">

  * Positional encoding -> token간 관계성을 표현하기 위함 
  * BERT처럼 0, 1, 2, 3 … 으로 위치를 표현하는 것이 아니라, 현재 token의 위치 대비 0번째, 1번째 2번째 … 상대적 거리 표현법을 사용 
  * Sequence 길이에 제한이 없어짐!

* **Permutation language modeling**

  <img width="588" alt="Screen Shot 2021-10-10 at 6 05 33 PM" src="https://user-images.githubusercontent.com/88299729/136694942-54c3f4d4-827f-42cf-9c60-b8492c03f095.png">

  * 기존 모델에서는 앞에서 순차적으로 학습을 하기 때문에 한 방향 학습 밖에 되지 않았다.
  * XLNET에서는 모든 순열 조합을 생성하여 그 조합들에 대해서 학습을 시키기 때문에 양 방향 학습의 효과를 볼 수 있다.

<br>

#### RoBERTa

BERT 구조에서 학습 방법을 고민!

1. Model 학습 시간 증가 + Batch size 증가 + Train data 증가
2. Next sentence prediction 제거 -> Fine-tuning과 관련 없음 + 너무 쉬운 문제라 오히려 성능 하락
3. Longer sentence 추가
4. Dynamic masking -> 똑같은 텍스트 데이터에 대해 masking을 10번 다르게 적용하여 학습



> 문제를 어렵게 만들고 어려운 문제를 학습한 모델이 성능이 좋다!



#### BART

<img width="400" alt="Screen Shot 2021-10-10 at 7 44 32 PM" src="https://user-images.githubusercontent.com/88299729/136695011-1602029c-a550-4114-8799-1a0108667d07.png">

Transformer Encoder-Decoder 통합 LM



#### T5

<img width="513" alt="Screen Shot 2021-10-10 at 7 45 51 PM" src="https://user-images.githubusercontent.com/88299729/136695025-a29bbb6a-ea86-4a60-bd97-1045c8ee3996.png">

TransformerEncoder-Decoder 통합 LM -> 현재까지의 끝판왕!



##### word 단위 masking이 아닌 phrase 단위 masking 사용

<img width="422" alt="Screen Shot 2021-10-10 at 7 49 13 PM" src="https://user-images.githubusercontent.com/88299729/136695034-295cc257-3155-4507-887e-3d7d430bdd3c.png">



#### Meena

<img width="362" alt="Screen Shot 2021-10-10 at 7 52 08 PM" src="https://user-images.githubusercontent.com/88299729/136695103-58092c87-29c5-4bd6-9001-84aafca8ccca.png">

대화 모델을 위한 LM

* 소셜 미디어의 데이터(341GB, 400억개의 단어)를 이용하여 26억개의 파라미터를 가진 신경망 모델을 이용한 end-to-end multi-turn 챗봇

* 챗봇의 평가를 위한 새로운 Metric인 SSA(Sensibleness and Specificity Average)를 제시

  <img width="328" alt="Screen Shot 2021-10-10 at 7 52 34 PM" src="https://user-images.githubusercontent.com/88299729/136695118-24697458-4d74-478b-88d2-a92f34ec18d6.png">

#### Controllable LM

<img width="427" alt="Screen Shot 2021-10-10 at 8 10 33 PM" src="https://user-images.githubusercontent.com/88299729/136695131-b99146c9-35cf-437d-9942-15e88f879a1b.png">

* PlugandPlayLanguageModel(PPLM)
  * 다음에 등장할 단어 ->확률 분포를 통해 선택
  * 내가 원하는 단어의 확률이 최대가 되도록 이전 상태의 vector를 수정
  * 수정된 vector를 통해 다음 단어 예측
  * 확률 분포를 사용하는 것이기 때문에, 중첩도 가능 (기쁨 + 놀람 + 게임) 
  * 특정 카테고리에 대한 감정을 컨트롤해서 생성 가능 
    * 정치적, 종교적, 성적, 인종적 키워드에 대해서는 중성적인 단어를 선택해서 생성 
    * 범죄 사건에 대해서는 부정적인 단어를 선택해서 생성 
  * 확률 분포 조절을 통해 그라데이션 분노 가능

<img width="299" alt="Screen Shot 2021-10-10 at 8 16 04 PM" src="https://user-images.githubusercontent.com/88299729/136695147-0033db03-8006-4d52-a131-8ecd3f8514d5.png">



* 한국어 BoW 실험

<img width="638" alt="Screen Shot 2021-10-10 at 8 20 42 PM" src="https://user-images.githubusercontent.com/88299729/136695174-a98826e4-f13c-4a47-ab7b-d2a4916cc5a7.png">

<img width="630" alt="Screen Shot 2021-10-10 at 8 21 07 PM" src="https://user-images.githubusercontent.com/88299729/136695190-601e2ff7-e349-416f-b154-74c9148fec09.png">

### 과연 자연어 to 자연어로 충분한가?

우리가 언어를 배울 때, writtenlanguage인 책만 보고 학습하나요? 태어나서 첫 마디를 뗄 때까지, 우리는 spokenlanguage를 통해 학습합니다. 또한 인간은 시각, 청각, 후각, 촉각, 미각 등의 모든 감각을 통해 세상을 학습합니다. 그렇다면 인공지능을 구현하기 위해 자연어 to 자연어로 충분할까?

<br>

### Multi-modal Language Model

Multi-modal을 활용한 언어모델들을 살펴봅시다.



#### 할머니 세포 (Grandmother cell)

<img width="620" alt="Screen Shot 2021-10-10 at 8 43 42 PM" src="https://user-images.githubusercontent.com/88299729/136695227-f17e0ea2-1c2d-4ac8-a3bf-73bd544aab04.png">

Philip Roth (1969)의 소설 Portnoy’s Complaint



* 즉, ’어머니’를 representation하는 conceptneuron을 모두 제거하니, 해당 concept에 대한 기억이 사라짐 
* JerryLettvin는 소설에서 아이디어를 얻어 할머니 세포라는 개념을 제시 (1969) 
* 이 세포는 1개의 단일 세포가 어떤 개념(concept)에 대해 반응 (e.g.할머니, 어머니)

<img width="122" alt="Screen Shot 2021-10-10 at 8 48 48 PM" src="https://user-images.githubusercontent.com/88299729/136695238-6f5c5d61-9814-4f47-9886-b2720c63174d.png">

#### Electrophysiological recording - Microelectrode arrays (MEAs)

<img width="611" alt="Screen Shot 2021-10-10 at 8 49 31 PM" src="https://user-images.githubusercontent.com/88299729/136695250-ca386037-deb0-430d-bb92-588b2a6a28b2.png">

#### Halle Berry neuron

<img width="653" alt="Screen Shot 2021-10-10 at 8 50 08 PM" src="https://user-images.githubusercontent.com/88299729/136695263-ebd4b6f4-338a-4f65-928e-3f8e2adb3002.png">

#### LXMERT

<img width="642" alt="Screen Shot 2021-10-10 at 9 03 01 PM" src="https://user-images.githubusercontent.com/88299729/136695369-e78d59ab-4e98-4bee-9c7b-025156d6f9ca.png">

* Cross-modal reasoning language model 

  (Learning Cross-Modality Encoder Represen - tations from Transformers)

* 이미지와 자연어를 동시에 학습!

<img width="572" alt="Screen Shot 2021-10-10 at 9 03 55 PM" src="https://user-images.githubusercontent.com/88299729/136695386-df8e5fd8-3b1b-46f3-8316-aba60fdfee91.png">

* 이미지 feature - 자연어 feature가 하나의 모델에 반영됨

#### ViLBERT

<img width="490" alt="Screen Shot 2021-10-10 at 9 04 37 PM" src="https://user-images.githubusercontent.com/88299729/136695407-a1d2cd38-08db-4f42-8b06-6083b9e03949.png">

BERT for vision-and-language

#### Dall-e

자연어로부터 이미지를 생성해내는 모델

e.g. 아보카도 모양의 안락 의자

<img width="368" alt="Screen Shot 2021-10-10 at 9 05 45 PM" src="https://user-images.githubusercontent.com/88299729/136695449-89a7637a-5533-4547-8690-aa171cff7811.png">

e.g. 아보카도 모양의 램프

<img width="391" alt="Screen Shot 2021-10-10 at 9 06 06 PM" src="https://user-images.githubusercontent.com/88299729/136695459-dff4a8a2-65c2-4c38-bc52-1c7cbf4d0889.png">

1. VQ-VAE를 통해 이미지의 차원 축소 학습

<img width="501" alt="Screen Shot 2021-10-10 at 9 07 01 PM" src="https://user-images.githubusercontent.com/88299729/136695480-b2436514-1013-4851-bfbd-a7ebd1d1b6b4.png">

2. Autoregressive 형태로 다음 토큰 예측 학습

<img width="600" alt="Screen Shot 2021-10-10 at 9 07 14 PM" src="https://user-images.githubusercontent.com/88299729/136695495-d301d219-744d-41a3-ad7e-af8ebbc4cf17.png">

