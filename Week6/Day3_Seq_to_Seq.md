## Sequence to Sequence with Attention

![화면 캡처 2021-09-09 013104](https://user-images.githubusercontent.com/88299729/132549533-d5573f97-1df2-451a-8b8c-99e2d2924071.png)



sequence data를 입력으로 받고 sequence data를 출력하는 모델이다.

* 이러한 방법을 사용 했을 때 문제점 : 마지막 time step vector에 모든 정보를 압축하고 저장해야 한다.
* LSTM, GRU를 통해서 해결됐다고 하더라도, 오래된 정보는 변질되거나 소실 될 확률이 높다.
* 과거의 트릭은 순서를 반대로 뒤집어서 학습을 시켜주었다.



### Sequence to Sequence 의 기본적인 모델 구조

![화면 캡처 2021-09-09 013612](https://user-images.githubusercontent.com/88299729/132549605-911f76e6-9ef6-4675-8868-011190202fac.png)

입력 데이터를 다 읽은 후에 출력을 시작하는 Many-to-Many 모델이 여기에 속한다.



### Attention!



![image](https://user-images.githubusercontent.com/88299729/132554107-d7972187-57b0-41c2-bbbf-dad93bd782bf.png)



#### 동작 방식

1. encoder RNN에서 각 단어들에 대해 encoding vector를 만들고, 학습한다.
2. 마지막 time step에서 만들어진 time step vector는 decoder에 h<sub>0</sub> 입력으로 들어간다.
3. decoder의 입력 x<sub>1</sub>과 동작하며 h<sub>1</sub><sup>d</sup>를 만들게 된다. 
4. encoder hidden state vector와 decoder hidden state vector를 내적하여 scores 값을 구한다.
5. softmax를 통해 상대적 확률 값으로 만들고, 어느 값이 output으로 적합한지 판단한다.



![화면 캡처 2021-09-08 150323](https://user-images.githubusercontent.com/88299729/132555654-cf624060-a22e-4bcd-98a5-9bc1175e5ca8.png)



* attention module의 output과 decoder hidden state vector 가 concat 되어 최종 예측 값을 만든다. 
* decorder hidden state vector 는 attention 과 예측 값 추론 두 곳에서 모두 쓰인다.



![화면 캡처 2021-09-08 220531](https://user-images.githubusercontent.com/88299729/132556861-1ce26ec6-bde7-4453-a50a-2680a5bca886.png)



#### Attention 구조에서의 back propagation

Attention output이 나온 부분과 decoder 부분, 두 방향으로 모두 진행이 된다. 이 방식으로 진행됨으로서 Encoder-RNN으로 가는 back propagation shortcut이 생긴 것과 같다.

* attention이 없을 때에는, 잘못된 출력이 된 경우, 그것이 encoder에 초반 hidden state vector까지 가야하는 경우 가야 할 길이 멀었지만, Attention을 씀으로서 지름길이 만들어졌다.



#### Teacher forcing

학습이 완료될 때까지 올바른 정답(ground truth)만 주게 되는데, 이를 teacher forcing 이라고 한다.

ex) decoder의 output이 다음 input으로 들어가는 inference 방식은 teacher forcing 이라고 볼 수 없다.



#### decoder와 encoder의 내적을 통해 유사도를 구했던 방법의 확장된 방법들



![화면 캡처 2021-09-08 234437](https://user-images.githubusercontent.com/88299729/132557290-80a1a72e-f60f-4c38-840a-8ce925c63544.png)



* 유사도를 구하기 위해 내적을 진행하는 행렬들 사이에 특정 행렬을 넣음으로서, 연산을 진행하는 hidden state vector에 가중치를 줄 수 있다. 이 경우, back propagation을 통해 사이에 들어간 특정 행렬 또한 학습하게 된다.

![화면 캡처 2021-09-09 001047](https://user-images.githubusercontent.com/88299729/132558241-14cc5daf-dfef-4d5a-9eee-a2ef423ce14d.png)

* encoder hidden state vector와 decoder hidden state vector를 concat 하여 MLP(Multi Layer Perceptron)과 같은 학습을 시켜 scalar 값으로 변환한다.

  