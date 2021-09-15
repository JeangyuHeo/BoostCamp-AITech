## Self-supervised Pre-training Models

### GPT-1

![화면 캡처 2021-09-16 005905](https://user-images.githubusercontent.com/88299729/133468755-d33d90a4-f514-4c5b-a490-2dab6fd9536b.png)

다양한 special 토큰을 제안해서, 심플한 task 뿐만 아니라 다양한 task를 커버하는 통합된 모델을 제안했다.



#### 동작 과정

* Task classifier에서 어떤 작업을 하는지 분류한다.
* sentiment analysis, classification 와 같은 input sequence가 1개인 경우, text 앞에 start token, 뒤에는 extract token을 넣는다.
  * sequence를 transformer를 통해 word별로 encoding을 한 후, extract 토큰을 linear transformation 하여 최종 결과를 얻는다.
* Entailment와 같은 논리적 내포 관계가 있어 input sequence가 2개인 경우, 앞에 start token, 두개의 논리 사이에 delimiter 토큰, 마지막에 extract token을함께 넣어서 sequence를 만든다.
  * 마찬가지로 extract 부분에 논리 관계를 이해한 정보가 들어 있다.

* 추가적으로 우리 task 를 위한 layer를 붙히고 random initialization 해준다.
* main task인 downstream task를 하기 위한 학습 데이터를 통해 전체 network를 학습하게 된다.
* 추가로 붙힌 layer는 random initialization 되기 때문에 충분한 학습이 되어야 하지만, transformer(이미 학습된 부분)은 learning rate를 상대적으로 작게 줌으로서 큰 변화가 일어나지 않도록 한다.
* language modeling, pre-train 단계에서 쓰는 데이터는 labeling 이 필요하지 않은 데이터이기 때문에 많은 양의 데이터를 통해서 simple한 task인 다음 단어를 예측하는 task를 통해 모델을 학습 할 수 있다.
* 예를 들어, 문서 분류의 경우에는 labeling이 필요하고, 데이터가 비교적 적을 수 밖에 없다. 이를 해결하기 위해 pre-trained step에서 대규모 데이터를 통해 별도의 label이 필요하지 않은 self supervised learning이라고 부르는 framework를 통해 대규모 데이터로부터 얻을 수 있는 지식을 소량의 데이터가 있는 target task에 전이 학습 형태로 활용하여 성능을 향상시킨다.



### BERT

![화면 캡처 2021-09-16 013226](https://user-images.githubusercontent.com/88299729/133484507-084fe1d3-fe76-423f-9771-56ab9c652431.png)



가장 널리 쓰이는 pre-trained model이며, 일부 단어를 맞추는 task를 진행하며 학습한다.



#### Motivation

* GPT-1의 경우, <sos> i study math 문장이 있을때, 순서대로 예측을 진행한다. 이렇게 되면 RNN과 마찬가지로 전후 문맥을 고려하지 못하고, 이전 문맥만 파악하게 된다.
* bi-directional language model을 하게 되면 단어들이 cheating을 하게 된다는 문제점이 있다.



#### Masked Language Model (MLM)

좌우를 다 본 후 예측하여 유의미한 예측 과 지식을 가지게 한다.

* 빈칸을 뚫고 그것을 맞추는 식으로 학습이 진행된다.
* 이때, 몇 퍼센트의 단어를 mask된 단어로 표시해야 할지는 hyper parameter이다. 15% 가 적당하다고 한다.
* 15% 보다 높으면 각각의 자리의 단어를 맞추기에 충분한 정보가 제공되지 못한다.
* 작게하면 100 단어를 읽어서 1단어만 맞춘다고 가정하면, 100단어를 읽어드려서 Transformer encoding하는 과정이 시간적으로 학습의 과정에서도 많은 계산을 요구한다. 즉, 효율이 떨어지고, 속도가 느리다.



#### Masked Language Model 방식의 문제점

* [MASK]에 익숙해진 model이 나올텐데, 특정 downstream task에서는 [MASK]라는 토큰은 더 이상 나오지 않는다.
* pre-training에서 주어진 데이터의 양상이나 패턴이 downstream task 입력 문장과는 다른 특성을 보이고, 상이한 차이점이 학습을 방해하거나 transfer learning 효과를 최대한 올리는데 문제가 된다.



#### Masked Language Model의 문제 해결 방안

총 100개의 단어가 있고 mask 처리 되어야 할 단어가 15개가 있다고 가정한다.

* 80%인 12개 정도는 [MASK]와 같은 특수한 토큰으로 치환하여 해당 단어를 맞추도록 한다.
* 10% 1.5개는 random word 로 바꾼다. 해당 단어가 mask가 아니라 regular한 word하더라도 단어를 원래 있어야 하는 단어로 잘 복원 할 수 있도록 한다.
* 10% 1.5개는 전혀 바꾸지 않고 그대로 넣어서 소신있게 예측 할 수 있도록 한다.



#### Next sentence prediction 기법

문장 level에서의 task에 대응하기 위한 pre-trained 기법을 제시했다.

* 하나의 글에서 두개의 문장을 뽑는다.

* 그 두 문장을 연속적으로 이어주고 문장 사이에는 [SEP] (seperate token)을 추가해준다.

* 문장이 끝날 때에도 추가해준다.

* 다수의 문장 level에서의 예측 task를 수행하는 token으로서 [CLS] (classification token)토큰을 문장의 맨 앞에 추가한다.

  * CLS token은 GPT-1의 extract token으로 생각하면 된다.

  



#### 다음 문장으로 적합한지 부적합한지 Task

![화면 캡처 2021-09-16 023144](https://user-images.githubusercontent.com/88299729/133484600-0c19d02b-f562-4895-bb27-83cacd834db9.png)

label이 필요로 하는 task가 아닌 입력데이터만으로 예측을 수행 할 수 있는 그런 task를 학습시키기 위해 주어진 두개의 문장이 연속적인 순서로 나와야 되는 문장인지, 연속적인 문장으로 나올 수 없는 문장인지를 예측하는 binary classification 수행하는 task 추가했다.



* CLS token 과 SEP token이 추가 되어진 채로 transformer를 통해 encoding 한다.
* mask 자리에 해당하는 토큰에서는 해당하는 encoding vector를 가지고 mask 자리의 단어를 예측한다.
* CLS 토큰은 이에 해당하는 encoding vector를 가지고 output layer를 두어서 binary classification 수행한다.
* 이때, ground truth는 인접한 문장인지 아닌지이다.



#### segment embedding

![화면 캡처 2021-09-16 023827](https://user-images.githubusercontent.com/88299729/133484710-6d268f55-29fa-4aa8-9528-95c177a23166.png)

문장 level 에서 어떤 position, index인지를 반영한 vector이다. position embedding과 함께 token embedding vector에 더해준다.





#### BERT 요약

![화면 캡처 2021-09-16 023630](https://user-images.githubusercontent.com/88299729/133484686-349e5a22-60a4-4a12-a4b0-32ac4a6eeedf.png)



* L = block 수, A는 각 layer별 head 수, H는 encoding vector의 차원 수
* BERT 가 GPT-1보다 3배정도 많은 데이터로 학습을 시켰다.
* Batch size는 BERT가 GPT-1보다 더 크다.
* 큰 사이즈의 batch를 사용하게 되면 최종 모델 성능이 더 좋아지고 학습도 안정화 된다.
* GPT-1는 learning rate가 5e-5로 고정이고, BERT는 task 마다 optimize 해줘야한다.



### Machine Reading Comprehension (MRC,  Question Answering)

![화면 캡처 2021-09-16 024156](https://user-images.githubusercontent.com/88299729/133484745-c5ab150a-8f2a-4602-a276-92971347866c.png)



#### SQuAD dataset 1.1

![image](https://user-images.githubusercontent.com/88299729/133484886-cb5817d6-d44f-4cdd-b85b-3c7bf3f32121.png)

cloud sourcing을 통해 만들어진 dataset 이다. 이 데이터셋으로 학습을 시키고 성능 평가를 하는 것이 일반적이다.



#### MRC 동작 과정 

vector들에게서 정답에 해당할 것 같은 위치, 즉, 특정한 문구의 위치를 찾아야한다.

1. 단어별 word encoding vector가 나온다. 
2. word encoding vector를 공통된 output layer를 통해서 scalar 값을 뽑도록 한다. 각각 word encoding vector가 2차원 vector로 나온 경우, output layer는 FC layer를 통해 scalar 값으로 만들어준다.
3. 가령, 124개의 단어가 있다면 124개의 score 값이 있을 것이고 이를 softmax 통과시켜주면 ground truth로서 정답의 첫번째 단어에 해당하는 그 확률 값이 100%에 가까워지도록 softmax loss 를 통해서 학습하게 된다.
4. 끝나는 시점도 예측해야한다. starting point를 찾는 layer와 동시에 end point를 찾는 작업을 동일하게 진행한다.



#### SQuAD dataset 2.0

![image](https://user-images.githubusercontent.com/88299729/133484933-e4d79af5-6611-4ecb-80c3-a2400d0a7868.png)

* 답이 없는 경우의 dataset까지도 원래 있던 데이터에 포함을 했다.

* 답이 있다 없다를 찾는 task의 경우 질문과 paragraph 둘 다를 확인해야 하는 task이고, [CLS]를 활용 할 수 있다.

* [CLS] 토큰으로 먼저 답이 있는지 없는지 판단을 한 후에 위의 과정을 통해 정답을 찾아낸다.



#### 다수의 문장을 다루어야 하는 Task

다음에 나와야 하는 적절한 문장을 찾는 경우를 예로 들 수 있다.

* [CLS] token을 사용한다.
* 비효율적이긴 하지만, 각 문장들과 하나하나 concat한다.
* encoding을 진행한다.
* [CLS] 값을 scalar 값으로 변환하여 softmax를 통과시킨다. 
* 정답인 부분을 ground truth로 설정하고 학습 결과가 100% 나올 수 있게 학습시킨다.



#### BERT의 특성

![화면 캡처 2021-09-16 025311](https://user-images.githubusercontent.com/88299729/133484785-9e6b4725-8ae7-4a4f-b46f-cf3f8898160a.png)

Parameter 의 양을 늘리면 끊임없이 성능이 좋아진다.