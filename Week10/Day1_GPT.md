## GPT 언어 모델

### 1. GPT 모델 소개

BERT는 Transformer의 Encoder, GPT는 Decoder를 이용하여 만들어졌다.

![화면 캡처 2021-10-10 001009](https://user-images.githubusercontent.com/88299729/136665982-95d5b8d6-8e65-4a4f-a5ce-5483031c3263.png)

그 중, 이번에는 GPT언어 모델에 대하여 소개한다.

![화면 캡처 2021-10-10 001025](https://user-images.githubusercontent.com/88299729/136665986-9e30844d-7098-4414-a421-212e4d4016f0.png)



#### GPT 모델을 통한 다양한 Task를 처리하는 법

![화면 캡처 2021-10-10 005335](https://user-images.githubusercontent.com/88299729/136666019-ef227254-0601-40a4-af77-1d6f04962af5.png)

#### GPT 모델의 특징

* [자연어 문장 -> 분류] 성능이 아주 좋은 디코더인 GPT 
* 덕분에 적은 양의 데이터에서도 높은 분류 성능을 나타냄 
* 다양한 자연어 task에서 SOTA 달성 
* Pre-train 언어 모델의 새 지평을 열었음 -> BERT로 발전의 밑거름 
* 하지만 여전히, 지도 학습을 필요로 하며, labeled data가 필수임 
* 특정 task를 위해 fine-tuning 된 모델은 다른 task에서 사용 불가능

![화면 캡처 2021-10-10 005600](https://user-images.githubusercontent.com/88299729/136666044-576cb370-5b03-441c-bc8e-34f7e36906af.png)

#### GPT 모델 자연 학습

![화면 캡처 2021-10-10 005708](https://user-images.githubusercontent.com/88299729/136666050-995565ca-ebeb-48d7-ba22-9d753c46566a.png)

위와 같은 문장을 학습하게 되면 '놀란' 이라는 것에 대해서 따로 학습을 하지 않아도 자연스럽게 문맥적으로 학습하게 된다. 또한, 엄청 큰 데이터셋을 사용하면 자연어 task를 자연스럽게 학습하게 된다.



#### NLP 학습의 새로운 제안

![화면 캡처 2021-10-10 005834](https://user-images.githubusercontent.com/88299729/136666103-a44ac1dc-b6e6-4908-b83d-37f9a3648181.png)

#### GPT1 & GPT2

![화면 캡처 2021-10-10 010251](https://user-images.githubusercontent.com/88299729/136666134-c183a442-6253-4298-b302-bb00d17a46f6.png)

#### GPT 모델의 의미

![화면 캡처 2021-10-10 010313](https://user-images.githubusercontent.com/88299729/136666142-f2ca2e32-4edf-4cc3-94ae-903949e5b8c2.png)

* 다음 단어 예측 방식에서는 SOTA 성능
* 기계독해, 요약, 번역 등의 자연어 task에서는 일반 신경망 수준
* 하지만! Zero, One, Few-shot learning의 새 지평을 제시!



#### GPT3의 성능

![화면 캡처 2021-10-10 010545](https://user-images.githubusercontent.com/88299729/136666156-b01237f4-158e-459f-98f7-f5c7cc932dd1.png)

### 2. GPT의 응용

#### 상식 Q&A

![화면 캡처 2021-10-10 010705](https://user-images.githubusercontent.com/88299729/136666160-337f3083-1c50-489b-8093-3fa4855f23ab.png)

#### 텍스트 데이터 파싱

![화면 캡처 2021-10-10 010755](https://user-images.githubusercontent.com/88299729/136666163-fa0bce4a-219b-43ea-a095-9984990767f2.png)

#### 의학

![화면 캡처 2021-10-10 010807](https://user-images.githubusercontent.com/88299729/136666169-fb91bbee-d859-40fa-a852-8c9e322068b5.png)