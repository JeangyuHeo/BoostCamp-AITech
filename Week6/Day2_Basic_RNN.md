## Basics of Recurrent Neural Networks (RNNs)



### RNN Basic Structure

![화면 캡처 2021-09-07 223103](https://user-images.githubusercontent.com/88299729/132359934-510e8cbc-adf1-476c-a9dd-2a0875ebe0fb.png)



### RNN에서는 어떻게 연산을 진행할까?

![화면 캡처 2021-09-07 224007](https://user-images.githubusercontent.com/88299729/132359966-394ed2be-b810-48a9-a0a7-d204277040bb.png)

이번 layer에 대한 input X<sub>t</sub> 와 저번 layer의 output h<sub>t-1</sub> 을 함께 활용하여 이번 layer의 연산을 진행한다.

![화면 캡처 2021-09-07 130818](https://user-images.githubusercontent.com/88299729/132360082-ae750353-3f61-4133-a000-10da24f69ecf.png)



### RNN의 종류

#### 1. one-to-one

![화면 캡처 2021-09-07 224131](https://user-images.githubusercontent.com/88299729/132360115-ef056524-44cc-4dc6-8938-55172cef18db.png)

​	일반적인 DNN과 다른 점이 없다.



#### 2. one-to-many

![화면 캡처 2021-09-07 224141](https://user-images.githubusercontent.com/88299729/132360146-7cb2ab7d-2ae2-450d-87e2-c13b29e09af0.png)

* 사진이나 그림의 장면을 보고 글로 표현하는 task가 이에 해당한다.
* 값을 넣는 부분 외에는 0으로 채워진 동일한 사이즈의 vector 값을 넣어주면 된다.



#### 3. many-to-one

![화면 캡처 2021-09-07 224152](https://user-images.githubusercontent.com/88299729/132360163-8b8a46c8-4d88-4d19-b6e0-8c4e28f78873.png)

* 감정 분류인 sentiment classification task가 이에 해당한다.



#### 4. many-to-many

![화면 캡처 2021-09-07 224204](https://user-images.githubusercontent.com/88299729/132360187-20b694df-e3ea-4071-9f1a-9531e7d70e4d.png) ![화면 캡처 2021-09-07 224216](https://user-images.githubusercontent.com/88299729/132360203-a071a8f8-7948-45a6-bb62-c5b23210ae8b.png)

* 입력 문장을 **다 읽고 예측**을 시작하는 모델과 입력 문장을 **받을 때마다 예측**을 하는 모델이 있다.
* 다 읽고 예측하는 경우, machine translation이 대표적인 task이다.
* 받을 때마다 예측하는 경우, video classification on frame level 이 대표적이다.



#### RNN의 학습은 어떻게 이루어질까?

![화면 캡처 2021-09-07 230748](https://user-images.githubusercontent.com/88299729/132360241-0c91b34b-7e0a-429b-bf87-b14eb4c308c3.png)

input X<sub>t</sub> 와 저번 layer의 output h<sub>t-1</sub> 선형 회귀와 tanh함수를 통해 연산을 진행한다. 이를 output y layer와 다음 hidden layer인 h<sub>t+1</sub> 로 보내게 된다. y에서는 W 선형 회귀를 통해 가장 큰 값이 내가 원하는 target이 될 수 있도록 parameter를 학습시킨다. hidden layer에 있는 W 또한 똑같은 원리로 동작한다.



#### 그렇다면 RNN은 어떻게 inference를 진행할까?

![화면 캡처 2021-09-07 230803](https://user-images.githubusercontent.com/88299729/132360302-c034a1ae-4f1a-491b-b814-26809c096255.png)

sequential data 의 첫 입력만 주고 그것의 output을 다음 input으로 사용하며 inference를 진행한다.



#### BPTT (Back Propagation Through Time)

![화면 캡처 2021-09-07 231149](https://user-images.githubusercontent.com/88299729/132360324-4411f2db-8105-4e7b-93a1-43476529d132.png)

실제로 한번에 연산을 할 수 있다면 좋겠지만, 현실에서는 하드웨어의 한계로 인해 일정한 크기로 끊어서 학습을 시키는 방식을 사용하는데, 이를 'BPTT'라고 한다.



### RNN 의 문제점

* 동일한 maxrix를 연산을 매번 곱해지기 때문에 back propagation 을 진행 할 때, gradient가 vanishing 또는 exploding 할 수 있다.



![화면 캡처 2021-09-07 231329](https://user-images.githubusercontent.com/88299729/132360340-81295827-545c-4b3e-8b8b-1ca8d40ee301.png)



* 거듭제곱의 형태로 gradient가 빠르게 감소함으로서 뒤쪽의 time step까지 유의미한 gradient signal을 전달 할 수 없다.

![image](https://user-images.githubusercontent.com/88299729/132360701-92c22c11-e103-416f-8cd8-d186d5ae890f.png)



## LSTM (Long Short-Term Memory)

RNN에서 gradient vanishing 과 exploding 문제를 해결하기 위해서 만들어진 모델이다. 즉, RNN 보다 나중까지 data가 잘 보존된다.

![화면 캡처 2021-09-07 232026](https://user-images.githubusercontent.com/88299729/132369641-b55760c4-e9b0-49b6-b9dc-2bcf69da55a8.png)



### LSTM의 중요한 2개의 States

#### 1. Cell state vector

* 우리가 필요로 하는 데이터를 모두 가지고 있는 완성도 있는 데이터

  ex) "Hello" 라는 출력을 할 때, Cell State는 "의 끝 마무리를 지어야 한다는 정보를 계속 가지고 있다.

#### 2. Hidden state vector

* cell state vector를 한번 더 가공해서 이번 layer에서 노출되어야 하는 것만 필터링 된 데이터

  ex) "Hello" 라는 출력을 할 때, 이번 출력에 의미 없는 " 정보 보단 인접한 문자에 대한 가중치 정보를 가진다.

  

### LSTM의 중요한 4개의 gates

cell state 에 정보가 **얼마나 흐르게 할지 제어**하기 위해 존재한다. 즉, 게이트란 cell state vector와 hidden state vector를 계산하기 위한 **중간 결과물**이다.



![화면 캡처 2021-09-07 232514](https://user-images.githubusercontent.com/88299729/132369697-e67983e7-5b80-4027-8c2f-0f6497a387af.png)

#### 1. Input gate

![화면 캡처 2021-09-07 234922](https://user-images.githubusercontent.com/88299729/132369791-25664d12-eafd-4863-ae7b-a2829b27d1cd.png)

x<sub>t</sub>와 h<sub>t-1</sub> 의 선형 결합을 통해 만들어진 output vector에 sigmoid를 취해준다. 이를 C<sub>t</sub> 와 곱해준다.

#### 2. Forget gate

![화면 캡처 2021-09-07 234855](https://user-images.githubusercontent.com/88299729/132369753-909ca616-d7a9-4ab6-93e8-c353d4bee326.png)

x<sub>t</sub>와 h<sub>t-1</sub> 의 선형 결합을 통해 만들어진 output vector에 sigmoid를 취해준다. 이 값을 cell state vector 값에 곱해줌으로서 일정 값을 잊어먹는 효과는 낸다.

#### 3. Output gate

![화면 캡처 2021-09-07 234939](https://user-images.githubusercontent.com/88299729/132369826-44b297e9-a3e2-4193-ad35-633a84babe32.png)

x<sub>t</sub>와 h<sub>t-1</sub> 의 선형 결합을 통해 만들어진 output vector에 sigmoid를 취해준다.

#### 4. Gate gate

![화면 캡처 2021-09-07 234922](https://user-images.githubusercontent.com/88299729/132369791-25664d12-eafd-4863-ae7b-a2829b27d1cd.png)

xt와 ht-1 의 선형 결합을 통해 만들어진 output vector에 tanh 함수를 취해준다. 이 값은 C<sub>t</sub> 로 사용된다.



#### 최종 H<sub>t</sub>

![화면 캡처 2021-09-07 234939](https://user-images.githubusercontent.com/88299729/132369928-c74f345a-5803-4b9f-b969-562fa127b6e9.png)

* C<sub>t</sub> 에 tanh을 취해주고, O<sub>t</sub> 에 sigmoid가 취해짐으로서 cell state 와 특정 dim 별로 각각 적정한 비율만큼 작게 만들어서 최종 H<sub>t</sub>를 만든다.
* C<sub>t</sub>는 기억해야 할 모든 정보를 담은 것이다.
* H<sub>t</sub> 에는 지금 현재 time step에서 예측 값을 output layer의 입력으로 사용하기 위해 직접적으로 필요한 값만 가지고 있다. 필터링 된 것과 같다.



## GRU (Gated Recurrent Unit)

![화면 캡처 2021-09-08 000539](https://user-images.githubusercontent.com/88299729/132369950-37b61807-42ac-4db3-be20-f97b87c4ef9c.png)

* cell state vector와 hidden state vector를 일원화 하여서 hidden state vector만 존재한다.
* LSTM과 비교해서 적은 메모리 요구량과 빠른 계산 시간이 확보되도록 제작되었다.
* h<sub>t</sub> 값을 구하기 위해 1-z<sub>t</sub> 를 사용했다는게 큰 특징이다.
* 가중 평균의 형태로 연산이 된다.



## 최종 Summary

![화면 캡처 2021-09-08 000549](https://user-images.githubusercontent.com/88299729/132369978-0cad56eb-8c17-448a-a3b9-c6a8baf9d6c0.png)

* 다양한 길이를 가질 수 있는 sequence data에 특화된 유연한 형태의 딥러닝이다.
* Vanilla RNN 구조가 간단하지만, 학습 시에 gradient vanishing, exploding 문제가 있어서 잘 사용되지 않는다.
* 이를 보완한 모델이 LSTM, GRU 이다.
* cell state vector, hidden state vector 각 스텝에서 업데이트 하는 과정이 덧셈에 기반하는 연산이기 때문에 gradient의 큰 변화가 없어서 vanishing, explosion, long term dependency 문제를 해결 할 수 있었다.

