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



