## Advanced Self-supervised Pre-training Models



### GPT-2

![화면 캡처 2021-09-19 034120](https://user-images.githubusercontent.com/88299729/133905382-55cd600e-2506-496b-b1e8-7027f3e51756.png)

#### GPT-2에 대한 정보

* GPT-1에서 Transformer 모델을 더 많이 쌓았고, Language modeling task model(다음 단어 예측)을 기본 task로 한다.
* 좋은 quality의 data를 사용하였다.
* 'The Natural Language Decathlon : Multitask Learning as Question Answering' 이 논문에서 **모든 종류의 자연어 처리 task는 question answering으로 처리 가능하다**는 아이디어에서 착안했다.
* 통합된 자연어 생성의 형태로 다양한 task를 통합해서 학습을 한 연구 사례이다.
* GPT-1에서는, 긍정, 부정을 classification 하는 sentiment classification을 하는 경우와 질문에 대응하는 대화 시스템에서의 문장을 생성하기 위한 dialog task 에서의 모델 구조가 매우 상이 할 것이다.
* 동작 방식은 굉장히 간단하다. 모델에게 질문을 한다. 예를 들어, '이 문장은 긍정인 것 같아? 아님 부정인 것 같아?', '위 글의 요약된 내용은 뭐야?'
* 퀄리티 높은 글로 학습시키기 위해서 'Reddit' 이라는 사이트에서 3개 이상의 좋아요를 받은 글에 외부 링크가 있는 경우, 거기 있는 document가 고품질의 좋은 document라고 판단하고 데이터로 사용하였다.

#### Preprocess

* Byte Pair Encoding (BPE)를 사용하여 embedding vector를 만들었다.



#### Modification

* 각 layer들을 random initialization 할 때, layer가 위로 가면 갈수록, layer의 index에 비례/반비례해서 initialization 되는 값을 더 작게 만들었다.
* 선형변환에 의한 값이 더 0에 가까워지도록 하여 위쪽에 있는 layer들의 하는 일이 점점 더 줄어들 수 있도록 한다.



#### Question Answering Task

zero-shot setting에서 이 task를 진행하여 55 정도의 F1-score가 나왔고, 대화형의 데이터로 fine-tuning 을 한 후에는 89의 F1-score가 나왔다.

> Zero-shot setting : 추가의 학습 데이터없이 pre-trained model로만 task를 진행하는 것



#### Summarization Task

![화면 캡처 2021-09-19 034139](https://user-images.githubusercontent.com/88299729/133905387-3cd8f6d7-fa65-48ad-b082-4c8ae6d09345.png)



마지막에 TL;DR:을 준다. 이게 나오면 그 앞에 대한 내용을 한줄 요약한다.
이 방법을 통해 summerization 을 zero-shot setting으로 진행 할 수 있었다. 



#### Translation Task

![화면 캡처 2021-09-19 034205](https://user-images.githubusercontent.com/88299729/133905400-56b8ea85-1bf2-45fe-9189-884b6e840848.png)

translation 또한, 주어진 문장이 있으면, 번역을 하고 싶은 언어로 뒷부분에 붙혀주면 zero-shot setting에서도 앞서 나온 문장을 불어로 어느정도 잘 번역해준다. 



### GPT-3

![화면 캡처 2021-09-19 034005](https://user-images.githubusercontent.com/88299729/133905404-643093f8-d300-4690-a0e2-228d5ab892e4.png)

GPT-2의 개선된 모델로서, 모델의 구조의 변화보다는 parameter 수를 대폭 늘려준 모델이다.



#### N-shot

![화면 캡처 2021-09-19 034258](https://user-images.githubusercontent.com/88299729/133905408-5a166c2a-362e-413b-afcc-1170e172fe66.png)



* **zero-shot**
  추가 학습 하나도 없이 pretrained 된 것만으로 translation
* **one-shot**
  추가적으로 1개의 예시 문장만 주고 translation
* **few-shot**
  여러개의 예시를 주고 translation



### ALBERT

* 경량화된 BERT 모델이라고 생각하면 된다.
* 성능이 좋아지면서 모델 사이즈를 줄이고, 학습 시간도 빠르게 만들었다.
* 새로운 문장 level에 self supervised learning pre-train task를 제안했다.



#### Factorized Embedding Parameterization

![화면 캡처 2021-09-19 034326](https://user-images.githubusercontent.com/88299729/133905414-cea0655b-b56c-42f4-8733-e792067511a7.png)



* Self attention을 쌓아나가는 모델들을 볼 때, residual connection으로 인해서 입력 dim이랑 동일하게 맞춰 주어야 한다.

* Dim 이 너무 작으면 정보를 담을 수 있는 공간 자체가 너무 작아지는 단점이 있을 수 있고, 너무 크면 그만큼 모델 사이즈도 커지고 연산량도 많이 증가하게 된다.

* 블럭을 쌓아가면서, 점점 더 하이레벨의 유의미한 정보들을 찾아나가는 과정이 deep learning이다.

* layer에서 word 별로 주어지는 문장 내에서 가지는 관계라든가, contexture한 정보들을 고려하지 않고, word별로 독립적으로 상수 형태의 vector로 주어지는 embedding layer 가 있을 때, embedding layer의 word가 가지는 정보는 위에서 전체 sequence 문장을 고려해서 각 단어들을 인코딩을 해서 그 정보를 저장해야되는 그 hidden state vector들에 비해서는 더 적은 양의 정보를 저장해도 충분 할 수 있을 수도 있다.

* 알버트에서는 embedding layer의 사이즈를 줄이는 새로운 방법 제시했다.

  ![화면 캡처 2021-09-19 034343](https://user-images.githubusercontent.com/88299729/133905425-debc9fee-a54d-4040-ae27-50d9b5050879.png)

* Embedding vector의 사이즈를 줄이고, 원래 사이즈로 만들어 주는 선형 변환을 한번 거친다.

* 500x100 의 matrix를 500x15 + 15x100 와 같이 쪼개주면, param 수가 굉장히 많이 감소하고, 연산량 또한 굉장히 적어진다.



#### Cross-layer Parameter Sharing

* **학습을 해야되는 param은 무엇일까?**

  선형 변환 행렬 W<sub>Q, K, V </sub> 가 head 개수만큼 있고, 그리고 최종적으로 원래 사이즈로 만들어주는 matrix

* 위의 matrix들을 하나의 matrix으로 share함으로서 BERT모델을 개선했다.
  성능 저하는 별로 없지만, parameter 수는 엄청 많이 줄어든다.



#### Sentence Order Prediction

기존의 pretrained 기법에 두가지가 있다.

1. masked language model(mask 된걸 찾는 task)
2. 두개의 문장을 separate token을 이용해서 concat해서 어떤 하나의 sequence로 만들어서 실제 연속된 문장인지, 관련이 없는 문장인지 구분하는 task



2번의 경우에, BERT에서 next sentence prediction 을 별로 실효성이 없다라는 의견이 있어서 빼고 학습을 시켜보았고, 성능의 차이는 미비했다.

그래서, 이를 개선한 방법으로,

ALBERT에서는 연속된 문장을 가져와서 그것을 정순으로, 또는 역순으로 binary classification task를 진행했다.

* 기존의 방식인 next sentence prediction같은 경우에는 같은 단어가 겹치지 않을 확률이 높다. 
* next sentence prediction의 경우, 자연스러운 논리적인 흐름, 미묘한 고차원적인 추론 과정이 아닌 단순히 내용적으로 볼 때, 겹치는 단어가 많이 있느냐 없느냐고 풀리기 때문에 예측하기 너무 쉽다.

### ELECTRA

![화면 캡처 2021-09-19 034355](https://user-images.githubusercontent.com/88299729/133905434-e97fe31a-1037-4ddf-a0e3-ca4c96ad4518.png)



#### Generator

language modeling(BERT)을 통해서 단어를 복원(예측)해주는 역할을 한다.



#### Discriminator

* GPT-2, GPT-3 처럼 self-attention block을 쌓은 모양을 하고 있다.

* generator의 결과에 대해서 replaced된 단어인지, 원래부터 있었던 단어인지를 구분해주는 역할을 한다. 이 과정은, Binary classification으로 진행된다.
* GAN 모델의 아이디어에서 착안했다.
* Discriminator 부분이 pre-training 모델 부분으로 사용된다.







### Light-weight Models



#### distillBERT

Teacher 모델의 distribution을 student 모델의 ground truth로 줌으로서 teacher의 학습을 잘 따라갈 수 있도록 한다.

#### TinyBERT

teacher 모델의 vector도 MSE를 통해 동일하게 따라갈 수 있도록 한다.



### Knowledge graph

신기술 동향으로서 공부해보면 도움이 될 것이다.
