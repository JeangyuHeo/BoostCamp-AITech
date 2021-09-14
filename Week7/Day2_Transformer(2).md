## Transformer

### Multi-head attention

![화면 캡처 2021-09-14 225845](https://user-images.githubusercontent.com/88299729/133305191-12e8eb0c-b2df-42b1-8071-89b62e5e9c63.png)

* 여러 버전의 attention을 수행한다. W<sub>Q</sub>, W<sub>K</sub>, W<sub>V</sub>가 여러쌍이 있다.

* 서로 다른 측면의 정보를 병렬적으로 뽑고 합치는 형태로 attention 모듈을 구성 할 수 있다.
* 각각의 head가 서로 다른 정보를 상호보완적으로 뽑는 역할을 한다.
* 여러개의 W<sub>Q</sub>, W<sub>K</sub>, W<sub>V</sub> 를 통해 얻어진 head를 concat해서 최종 head 값을 얻을 수 있다.
* concat 하여 만든 vector를 input size로 다시 바꿔줄 선형 변환이 있어야 한다. residual connection 연산을 하기 위해서이다.



![화면 캡처 2021-09-14 234015](https://user-images.githubusercontent.com/88299729/133305218-8b1b4961-5af6-4ada-a626-7e3134dfa5c0.png)



### Attention과 RNN의 메모리, 속도 비교



![화면 캡처 2021-09-15 001105](https://user-images.githubusercontent.com/88299729/133305264-95aaad9d-d234-40f8-aa1e-b4143ac57513.png)



* **메모리 요구량**

  * d는 hidden state vector의 dimension 으로 hyperparameter로서 사용자가 지정 할 수 있다.

  * n의 값은 입력 sequence 의 길이가 길면 길수록 임의로 고정된 값으로 사용 할 수 있는게 아니라 주어진 입력에 따라 가변적인 값을 가진다.

  Self Attention에서 길이가 긴 sequence 를 처리하게 되면 sequence 의 길이의 제곱에 비례하는 계산량과 메모리 사이즈가 필요하다.

  RNN에서는 sequence 길이에는 1차함수로서 비례하는 형태이다. 

  또한,

  * back propagation에서 사용하기 위해서 모든 key, query vector의 내적 값을 저장하고 있어야 한다.

  따라서, 일반적으로 self attention이 RNN보다 더 많은 메모리를 요구한다.



* **Sequential 한 데이터 처리 속도**

  * Self attention 은 sequence의 길이가 아무리 길더라도 GPU의 개수가 충분하면 모든 연산을 동시에 가능하다.
  * 반면에 RNN은 h<sub>t</sub>를 구하기 위해서는 h<sub>t-1</sub>이 필요하기 때문에 직렬적으로 O(n) 시간에 처리할 수 밖에 없다.

  따라서, self attention이 RNN보다 훨씬 빠르다고 할 수 있다.



* **가장 멀리 있는 단어에 대한 정보를 얻기 위한 거리**

  * self attention의 경우, 개별적으로 query, key, value vector를 통해서 바로 구할 수 있다.
  * RNN의 경우, 끝에서부터 끝까지 타고타고 가야하기 때문에 O(n) 만큼의 시간이 걸린다.

  따라서, self attention이 RNN보다 훨씬 빠르다고 할 수 있다.



### Add operation (Residual connection)

![화면 캡처 2021-09-15 013300](https://user-images.githubusercontent.com/88299729/133305292-033be621-7b4a-4bc9-8efb-3911f935afd6.png)

computer vision에서 깊은 neural network을 만들 때, gradient vanishing 문제를 해결하여 학습은 안정화시키면서 layer를 쌓아감에 따라 더 높은 성능을 보일 수 있게 하는 테크닉이다.

* 예를 들어, input vector가 (1, -4)라고 가정하고, output vector가 (2, 3) 라고 한다면 그 합인 (3, -1)이 최종 output vector가 된다.
* Residual connection으로 인해 multi-head attention 에서는 결국 입력 값 대비, 만들고자 하는 벡터의 차이 값만을 attention모듈에서 만들고 학습한다.
* 이를 위해, attention output vector의 사이즈를 resize해주어야 한다.



### Layer Normalization

![화면 캡처 2021-09-15 013709](https://user-images.githubusercontent.com/88299729/133305334-c07bd692-2ff0-41cc-b503-c2ddea3e118c.png)



주어진 다수의 sample 들에 대해서 그 값들의 평균이 0, 분산이 1로 만들어 준 후, 원하는 평균과 분산을 주입 할 수 있도록 하는 선형 변환이다. 이렇게 만들어 주기 위해서, 각 단어들에서의 평균과 분산을 구해서 사용한다.

* 학습을 안정화하고, 최종적인 성능을 끌어올리는데, 중요한 역할을 한다.

* Affine transformation 연산을 하는 경우, 각 단어의 같은 위치에 있는 vector 값들끼리 특정 함수 연산을 진행한다. 이때, y절편은 평균, x의 기울기의 제곱은 분산이 된다.

  ![화면 캡처 2021-09-15 013809](https://user-images.githubusercontent.com/88299729/133305355-2d1b1e19-b6ec-4f5f-8ff6-baf3892658a8.png)



### Positional Encoding

![image](https://user-images.githubusercontent.com/88299729/133305531-f2058b4a-5a1a-4fc8-a86d-62fd9c03388e.png)



각각의 encoding hidden state vector 값에서 query, key, vector를 구하여 encoding vector를 구하기 때문에, 순서의 관계없이 동일한 값이 나온다. 또한, RNN은 이전 hidden state vector를 input으로 받기에 자연스럽게 sequence 를 인식하지만, self attention 은 그렇지 못하다. 이를 해결하기 위해 positional encoding 을 사용한다.



* cos 함수, sin 함수와 같은 주기 함수를 주로 사용한다.
* 서로 다른 주기를 갖는 여러 함수들을 사용해서 거기서 발생된 특정 x값에 대한 함수 값을 x에 해당하는 index 의 sequence 값에 더해준다.
* 함수가 dim 개수만큼 있다.



### Learning rate scheduler

![화면 캡처 2021-09-15 015758](https://user-images.githubusercontent.com/88299729/133305429-0f6445b2-870a-434b-871e-c0e19943f348.png)

* Hyper parameter 로서, 최종 gradient 값이 더 잘 수렴하게 한다.
* Learning rate 값이 너무 크면 최저점에 도달하지 못하고 주변을 맴돌게 된다.
* 어느정도 학습이 진행된 후에는 서서히 learning rate를 줄여준다.



>  이렇게 위의 성분들로 만들어진 블록을 총 N번 학습을 시키게 된다.



### Encoding이 보여주는 패턴

![화면 캡처 2021-09-15 015818](https://user-images.githubusercontent.com/88299729/133305578-414705f5-7c41-469a-85c0-fcdd9b7651fa.png)



### Decoder

![화면 캡처 2021-09-15 015836](https://user-images.githubusercontent.com/88299729/133305600-57b39c61-30aa-4f44-8c29-98061010c5d5.png)

Encoder에서 만들어진 hidden state vector를 value, key 값으로 사용하여 output을 도출한다.



#### Decoding 순서

1. positional 정보가 추가된 shifted right output이 Multi-head Attention 을 통해 encoding 된다.
2. 이때, mask를 진행한다. (뒤에서 설명하겠다.)
3. 두번째 Multi-head attention에서는 첫번째 decoder attention의 hidden state vector가 query가 되고, encoding 단의 최종 output vector가 key, value로 사용된다.
4. encoding 을 진행한 vector는 encoder, decoder 의 정보를 골고루 가질 수 있다.
5. 이후 encoder와 동일한 과정으로 진행된다.



### Masked self attention의 기본 아이디어

![화면 캡처 2021-09-15 021119](https://user-images.githubusercontent.com/88299729/133305619-70c4353f-4eb5-471c-80c3-632572fce107.png)

* '나는 집에 간다' 라는 sequence 가 있고 학습시킨다고 가정하자!

* 이때, 입력은 <sos>, '나는', '집에' 가 들어간다.

* 모든 데이터 정보를 학습 당시에는 Batch processing 때문에 입력으로 같이 주기는 하나 <sos>를 query로 사용해서 attention module에서 수행을 할 때에는 접근 가능한 key, value값에서 '나는'과 '집에'는 제외에 주어야 한다.

  ![화면 캡처 2021-09-15 021816](https://user-images.githubusercontent.com/88299729/133305688-c3498314-5a00-489f-a889-9736e8586b16.png)

* 제외시켜주기 위해서, 제외 되어야 하는 항목에 -무한대를 더한다. 왜냐하면 softmax를 통해서 전부 0의 값이 나오기 때문이다.
* 나머지 0이 아닌 값들은 가중 합이 1이 되도록 한다.

![화면 캡처 2021-09-15 021844](https://user-images.githubusercontent.com/88299729/133305768-af581c13-13bc-4691-ab1d-f45b8649e2c4.png)

간단하게 설명하면, 

모두가 모두를 볼 수 있도록 한 후에 후처리적으로 보지 말아야 되는 부분들의 가중치를 0으로 만들어주고, 그 이후 value vector와 가중 평균을 내는 방식으로 변형한다.



### Experimental Results

![화면 캡처 2021-09-15 021855](https://user-images.githubusercontent.com/88299729/133305825-f1167db4-5e97-4383-9715-31fe99f44f59.png)

성능이 41정도라는게 굉장히 낮아보이지만, '나는 너를 좋아한다.' 와 '나는 너를 정말 좋아한다.' 등이 다른 문장으로 분류되는걸 생각해보면 실제로 체감되는 성능은 굉장히 좋다.

