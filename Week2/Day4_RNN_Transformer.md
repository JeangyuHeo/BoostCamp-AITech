## Recurrent Neural Network

![화면 캡처 2021-08-13 212724](https://user-images.githubusercontent.com/88299729/129357326-0b06c528-366e-4a4b-af64-0f7e98e9d011.png)

### Sequential Model 이란?

일상 생활에서 접하는 순서가 있는 대부분의 데이터 : 말, audio, video, 몸짓



#### sequential data의 특징

1. 길이가 언제 끝날지 모른다. 
2. 차원을 알 수가 없다.
3. FCL, CNN을 사용 할 수 없다.
4. 몇 개의 입력이 들어오든지 상관 없이 동작해야 된다.



#### 어려움 

sequential data의 특징을 고려해서 하나의 라벨을 얻어야 한다.



입력이 여러 개 들어왔을 때 다음 번 입력에 대한 예측을 해야되는데,

고려해야되는 **정보량이 점점 늘어**나는게 가장 큰 어려움이다.



#### Markov Model

* 가장  쉬운 방법이다.
* 바로 전 과거의 데이터에만 dependent하다.
* 많은 정보를 버릴 수 밖에 없다.



#### Latent Autoregressive Model

* 중간에 hidden state 가 있고 과거의 정보를 summarize한다.

* 이거를 잘 반영한게 RNN이다.

* 직전 데이터 뿐만 아니라 이전 데이터에도 dependent하다.



* 문제점
  1. short-term dependency - fixed rule로 과거의 데이터를 취합하기 때문에 먼 과거 데이터는 살아남기 힘들다. 
  2. sigmoid : gradient anishing ReLU는 gradient exploding 현상이 일어난다.



#### LSTM (Long Short Term Memory)

![화면 캡처 2021-08-13 213035](https://user-images.githubusercontent.com/88299729/129357597-79eec08b-c294-4786-b19b-1fd1c6db2e3f.png)

RNN의 한 모델이다.

x : input

h : hidden state

previous cell state : 내부에서만 흘러가고 0부터 t까지의 data를 summarize한다.

cell state : 컨베이어 벨트와 같다. 정보가 올라오면 조작공들이 잘 조작해서 다음에 넘긴다.



![화면 캡처 2021-08-13 213056](https://user-images.githubusercontent.com/88299729/129357642-cc33acff-0976-40c7-83ea-39a2fb3ea012.png)



* Gates

  1. Forget gate : 어떤 정보를 버릴지 정한다.
  2. Input gate : 어떤 정보를 올릴지(저장) 말지 정한다.
  3. output gate : 업데이트된 정보를 기반으로 output을 만든다.

  

* update cell : cell state에 버릴건 버리고 올릴건 올린다.



#### GRU

![화면 캡처 2021-08-13 213225](https://user-images.githubusercontent.com/88299729/129357703-92765d99-efb6-428f-a4a4-2be680127960.png)



LSTM과 달리 gate가 2개 밖에 없다.

cell state가 없고 hidden state가 cell state 역할까지 한다.

reset gate : forget gate와 비슷하다고 생각하면 된다.





## Transformer

#### Attention is All you need



<img width="415" alt="스크린샷 2021-08-14 오후 3 52 10" src="https://user-images.githubusercontent.com/88299729/129438138-16a7c8bb-f21f-463e-927b-b007a0a78a38.png">



Sequence한 데이터를 처리하고 Encoding, Decoding를 하는 과정

입력 sequence와 출력 sequence 는 단어와 숫자가 다를 수 있다.



**Self-Attention** 과 **feed-Forward Neural Network** 구조로 이루어져 있다.

3개의 단어가 들어오면 3개의 벡터를 다 찾는다.



#### Self-Attention

<img width="929" alt="스크린샷 2021-08-14 오후 3 52 31" src="https://user-images.githubusercontent.com/88299729/129438145-bca39b41-d5c9-4065-87b8-020b5527160e.png">

* 1개를 값을 구할 때 나머지 n-1개의 데이터도 같이 고려한다.

ex) X<sub>1</sub>의 vector를 구할 때 X<sub>2</sub>, X<sub>3</sub>의 데이터도 같이 활용한다.

* 작동 순서

  

  <img width="901" alt="스크린샷 2021-08-14 오후 3 53 27" src="https://user-images.githubusercontent.com/88299729/129438152-fec73a09-62e8-4a93-80c4-49eecbfe5e66.png">

  

  1. 각 단어에 대한 embedding vector를 만든다.
  2. 각 vector에 특정 행렬을 곱하여 encoding 하고자 하는 query vector와 나머지 n개에 대한 key vector를 구한다. 
  3. 그 두개를 내적하여 score vector 값을 구한다.
  4. i 번째 단어가 나머지 n-1개의 단어와 얼마나 유사도가 있는지, 관계가 있는지 정한다.
  5. Score vector가 나오면 한번 normalize를 해준다. (#key vector의 루트로 나눠준다.)
  6. softmax를 취해준다.



<img width="970" alt="스크린샷 2021-08-14 오후 3 53 50" src="https://user-images.githubusercontent.com/88299729/129438164-275775e3-8f99-4c74-8588-15bf6df4d9e0.png">



즉, value vector들의 weight를 구하는 과정이 각 단어에서 나오는 query vector와 key vector 사이의 내적을 normalize 해주고 softmax 해주고를 반복한다.



**Value vector와 softmax 출력 값의 weighted sum**이 최종적으로 얻고자 하는 encoding 값이다.



>  참고사항

1. 내적을 해야 하기 때문에 query vector하고 key vector는 차원이 같아야 한다. 
2. value와 output의 차원은 같다.
3. 입력, 출력이 고정되지 않는다.
4. 고로 더 많은 걸 표현 할 수 있다.
5. computation 양이 굉장히 높다



#### feed-Forward Neural Network

MLP랑 동일한 구조이며, 데이터 간의 dependancy는 없다.



#### Multi-Headed Attention



<img width="722" alt="스크린샷 2021-08-14 오후 3 54 16" src="https://user-images.githubusercontent.com/88299729/129438177-0ba5b4a3-50e5-41fc-8334-b7840a22c157.png">



**Multi-headed attention(MHA)**은 앞에서 이야기했던 attention 과정을 여러번 수행한다. **하나의 임베딩 벡터(입력)에 대해서 (Query,Key,Value) 벡터 셋을 여러 개 만든다**. 이 때문에 multi-headed(머리가 여러개)라는 이름이 붙었다.

* head의 개수와 encoding vector의 개수는 일치한다.
* 연산시에 embedding vector의 dim와 head의 dim 이 맞지 않는다면, embedding vector의 사이즈를 head 사이즈로 나누어서 연산한다.



<img width="924" alt="스크린샷 2021-08-14 오후 3 58 30" src="https://user-images.githubusercontent.com/88299729/129438184-1bce0aa9-b277-44f4-8060-e57efa5d6b6d.png">



#### Positional Encoding 



<img width="942" alt="스크린샷 2021-08-14 오후 4 05 35" src="https://user-images.githubusercontent.com/88299729/129438224-8daccc8b-b26c-4ee4-a3c7-7ba0282c052c.png">



Sequential한 데이터를 넣어주지만 반영되어 있지 않다. 이를 위한 **bias** 라고 생각하면 된다.

Ex) abcd 나 dcba나 encoding 한 값이 동일하다. 왜냐하면 order에 independent 하기 때문이다.



### Decoder



<img width="755" alt="스크린샷 2021-08-14 오후 4 00 03" src="https://user-images.githubusercontent.com/88299729/129438196-00b6a653-882b-4611-ad8a-8ab64d6d6879.png">



encoder의 마지막 층에서의 value 값과 score 값을 가지고 연산을 한다.



이 Encoder-Decoder Attention Layer는 MHA와 동일한 방식으로 동작하지만, **Query 벡터를 이전 Decoder에서 받아오고 Key, Value 벡터를 인코더 스택에서 받아온다**는 차이가 있다.

디코더의 마지막 층에서는, **디코더 스택의 출력물을 단어들의 분포로 만들어 내보낸다**. 
