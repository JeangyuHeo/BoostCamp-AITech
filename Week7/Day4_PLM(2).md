## Advanced Self-supervised Pre-training Models



### GPT-2



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

마지막에 TL;DR:을 준다. 이게 나오면 그 앞에 대한 내용을 한줄 요약한다.
이 방법을 통해 summerization 을 zero-shot setting으로 진행 할 수 있었다. 



#### Translation Task

translation 또한, 주어진 문장이 있으면, 번역을 하고 싶은 언어로 뒷부분에 붙혀주면 zero-shot setting에서도 앞서 나온 문장을 불어로 어느정도 잘 번역해준다. 



### GPT-3

GPT-2의 개선된 모델로서, 모델의 구조의 변화보다는 parameter 수를 대폭 늘려준 모델이다.



#### N-shot

* **zero-shot**
  추가 학습 하나도 없이 pretrained 된 것만으로 translation

* **one-shot**
  추가적으로 1개의 예시 문장만 주고 translation

* **few-shot**
  여러개의 예시를 주고 translation





### ALBERT

 

### ELECTRA



### Light-weight Models

