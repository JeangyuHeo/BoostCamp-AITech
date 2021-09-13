## Transformer

### Attention is all you need

![image-20210914003126697](C:\Users\82104\AppData\Roaming\Typora\typora-user-images\image-20210914003126697.png)



#### Attention module

기존에는 add-on module 로서 attention module 이 사용됐다면, Transformer에서는 LSTM이나 GRU와 같은 RNN 은 모두 걷어내고 Attention만으로 모든 부분을 대체했다. 즉, **순수하게 attention 만으로 sequence data를 받고, sequence data를 예측**한다.



#### RNN의 문제점

![화면 캡처 2021-09-14 005410](https://user-images.githubusercontent.com/88299729/133125933-af941745-8d45-4126-ad8b-69cc4e8d9810.png)

* Long term dependency problem
* gradient vanishing
* gradient exploding

멀리 있는 time step에서의 정보 전달은 변질과 손실이 많이 일어나 온전히 전달하기 어렵다.



#### Bi-directional RNNs

![화면 캡처 2021-09-14 005546](https://user-images.githubusercontent.com/88299729/133125976-8d4c463e-242c-4028-90f5-d51c503a94a1.png)



forward RNN : 문장을 앞에서부터 학습하는 RNN

backward RNN : 문장을 뒤에서부터 학습하는 RNN

* Forward RNN에서는 왼쪽 time-step에서는 오른쪽 time-step의 data 정보를 담을 수 없다. backward RNN을 추가해주고 각각 학습을 시켜 별개의 parameter을 생성해준다. 

* 특정 i 번째 hidden state에 대해서 2개의 RNN hidden state vector를 concat 해준다.
* 이렇게 연산 할 시, 주변 단어에 대해서 더 많은 정보를 가지고 있을 수 있다.



### Transformer



![화면 캡처 2021-09-14 015849](https://user-images.githubusercontent.com/88299729/133126036-3028e959-4216-444f-add7-7d0cf7df4a30.png)



**self attention** **모듈은 동일한 set의 vector에서 각 역할에 따라 linear transformation matrix W<sub>q,k,v</sub> 와 내적을 통해 Query, Key, Value 로 변환된다.**

* **Query vector** : 주어진 vector들 중에서 어느 vector를 선별적으로 가져올지의 기준이 되는 vector
* **Key vector** : query vector와 각 hidden layer에 대한 i개의 key vector 의 내적을 통해 가중치를 구한다.
* **Value vector** : 가중 평균을 구하기 위해서 사용된다. (가중 평균은 상대적 중요성이 강조된 평균)



![화면 캡처 2021-09-13 231541](https://user-images.githubusercontent.com/88299729/133126166-27d66ab4-f20a-4cfa-a6ba-831d828ae7ad.png)



![화면 캡처 2021-09-13 232059](https://user-images.githubusercontent.com/88299729/133126193-a8a67b44-2036-4bb7-baba-621c697df27a.png)



#### 연산의 순서

![화면 캡처 2021-09-14 015808](https://user-images.githubusercontent.com/88299729/133126080-b84f85ce-42ce-415f-baae-a8919b7e2223.png)

1. encoder hidden state vector에서 W<sub>q</sub>, W<sub>k</sub>, W<sub>v</sub> 를 내적함으로서 query, key, value vector를 구한다. 여기서, key와 value vector는 각각 자기들의 쌍이 있고, 1:1로 매칭된다.
2. 한 개의 기준 query vector를 각 key vector와 내적하여 score(가중치) 값을 구한다. 이 과정은, 어떤 vector 가 가장 높은 유사도를 가지고 있는지, 어느 것을 가져올지를 결정한다.
3. score 값을 softmax 를 통해 합이 1인 확률로 바꾸어준다.
4. 확률 값을 value vector와 weighted sum하여 최종 output 값을 구한다.



![화면 캡처 2021-09-14 001143](https://user-images.githubusercontent.com/88299729/133126100-bb734082-4378-4a0d-9a3f-520f6373c266.png)



#### Self Attention의 효과

* query vector와의 내적의 값만 높다면 time step의 거리가 멀었다 하더라도 손 쉽게 가져올 수가 있다.

* **long term dependency의 문제를 깔끔하게 해결**한 sequence encoding기법이다.
* 병렬적인 행렬 연산을 하는 특성 덕분에 RNN과 비교해서 **학습 속도가 빠르다**.



#### 차원은 어떻게 맞춰야할까?

score 값(가중치)은 **key vector와 query vector**의 내적을 통해서 구해진다. 따라서, **같은 차원의 vector**여야한다. **하지만**, **value vector**는 어차피 상수배가 되는 것이기 때문에 **차원이 달라도 연산에 아무 문제가 없다**.

따라서, 최종 차원은 d<sub>v</sub>로 나오게 된다.



#### d<sub>k</sub><sup>1/2</sup>로 나누는 이유



![화면 캡처 2021-09-14 015504](https://user-images.githubusercontent.com/88299729/133126233-b57f3936-6466-4ca6-9315-8dec672be633.png)



각 query, key 의 내적 값은 평균 0, 분산 1을 따른다. 그리고, 원래 값을 더하면, 분산 값도 더해지게 된다.

이때, key vector의 차원이 클 경우, 분산이 커지게 된다. 예를 들어 100이라고 하면 분산이 100이 된다.

softmax에서 분산이 클수록, 확률 분포가 큰 값에 몰리는 현상이 있고, 분산이 작을 경우, 고르게 분포한다.

따라서, key의 차원의 root로 나눠줌으로서 분산을 일정하게 유지시켜 주는 효과를 가져오고 학습이 안정화된다. 