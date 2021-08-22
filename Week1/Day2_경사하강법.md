## 경사하강법



#### 미분 (Differentiation)

![image-20210806190115371](https://user-images.githubusercontent.com/88299729/130360110-e2e4bde4-0a0a-4c7a-82e4-e0ef4acb8036.png)

* h 값이 0이 수렴함에 따라 x 점에서의 순간 변화율을 의미한다.
* 다변수 함수의 경우 필요한 변화율에 대한 변수에 대해서 미분을 진행한다.

다변수 함수의 경우 각 변수 별 편미분 값을 계산한 gradient 벡터를 이용하여 경사 하강/상승법에 활용 할 수 있다.



<img width="781" alt="image-20210807162648133" src="https://user-images.githubusercontent.com/88299729/130344921-0bfd2ca8-e3f7-42e0-aab8-d8c19fea8ae9.png">

##### 경사상승법 (Gradient ascent)

함수 값을 증가시켜야 하는 경우 : 미분 값을 x 값에 더해주는 것을 반복 함으로서 극대값을 구한다.



##### 경사하강법 (Gradient descent)

함수 값을 감소시켜야 하는 경우 : 미분 값을 x 값에 빼주는 것을 반복 함으로서 극소값을 구한다.



- 미분값 > 0이면, 증가하는 기울기에 있으므로 미분 값을 더하면,  *x*+*f*′(*x*)>*x* , 오른쪽으로 이동하여 함수 값이 증가한다.

- 미분값 < 0이면, 감소하는 기울기에 있으므로 미분 값을 더하면,  *x*+*f*′(*x*)<*x* , 왼쪽으로 이동하여 함수 값이 증가한다.

- 미분값 > 0이면, 증가하는 기울기에 있으므로 미분 값을 빼면,  *x*−*f*′(*x*)<*x* , 왼쪽으로 이동하여 함수 값이 감소한다.

- 미분값 < 0이면, 감소하는 기울기에 있으므로 미분 값을 빼면,  *x*−*f*′(*x*)>*x* , 오른쪽으로 이동하여 함수 값이 감소한다.

  

Day1에서 학습한 것과 같이 **선형** 모델의 경우에는 **무어-펜로즈 역행렬**을 통해 최소값을 구하는 것이 가능하다.

**BUT!** **비선형**의 경우에는 **경사하강법**을 이용해야 최소값을 구할 수 있다.



* TIP !

  **∇(nabla)** 를 *f*'(*x*) 대신 사용하며 **모든 변수**에 대해서 **동시에 업데이트** 하는 것을 의미한다.

  Ex)   

  ​		*f*(*x*, *y*) = *x*<sup>2</sup> + 2*y*<sup>2</sup>      ∇*f* = (2*x*, 4*y*)

  

  * gradient 벡터 ∇*f*(*x*,*y*) 는 각 점 (*x*,*y*)에서 **가장 빨리 증가하는 방향**과 같다.
  * 반대로, gradient 벡터 -∇*f*는 ∇(−*f*)와 같고, 이는 각 점 (*x*,*y*)에서 **가장 빨리 감소하는 방향**과 같다.

  

  <img width="253" alt="image-20210807165105019" src="https://user-images.githubusercontent.com/88299729/130344956-f35799ed-a8d2-4441-aa74-98bc95f6a54f.png">

  

  ### 선형 회귀 계수, 경사 하강법으로 구하기

  

  || *y* - *X*||*β*<sub>2</sub> 이 선형 회귀를 하고자 하는 목적식이라고 한다면,

  우리의 목적은 이를 **최소화하는 *β*** **값을 구하는 것**이라고 할 수 있다.

  

  <img width="477" alt="image-20210807170313593" src="https://user-images.githubusercontent.com/88299729/130344965-5e82cfe5-8232-444b-8c41-6f1d6205a7de.png">

  

  위와 같은 식으로 목적식을 표현 할 수 있다.

  

<img width="421" alt="image-20210807170501820" src="https://user-images.githubusercontent.com/88299729/130344972-92b8385c-6238-4344-9adf-1b5c4c4ee99a.png">

* 이때, 동작 원리를 이해하기 위해 편미분을 하는 것을 직접 유도해보는 것을 권장한다.

> 이해를 돕기 위한 한가지 포인트

데이터가 n가 있다는 가정 하에 미분을 하기 때문에 1/n 나누어 주는 연산을 해준 후에 root를 취해준다.



![image-20210807174311357](https://user-images.githubusercontent.com/88299729/130344980-bdff371f-45de-427b-8c25-ede02844fc76.png)

이 과정을 결과로서, 목적식을 최소화하는 *β*를 구하는 식을 다음과 같이 구할 수 있다.

<img width="296" alt="image-20210807174941860" src="https://user-images.githubusercontent.com/88299729/130344989-d5b3b53e-a938-4827-a1ca-169311746720.png">



* 실제 계산을 할 경우 L2-Norm 을 최소화 하는 것이나 (L2-Norm)<sup>2</sup> 을 최소화 하는 것이나 같기 때문에 연산이 간단한 (L2-Norm)<sup>2</sup> 을 사용한다. 이는 

<img width="295" alt="image-20210807175354748" src="https://user-images.githubusercontent.com/88299729/130344997-76be518c-a4d4-4111-ade1-0e10b37ddcc0.png">

으로 나타낼 수 있다.



### 확률적 경사 하강법 (Stochastic Gradient Descent : SGD)

경사하강법(Gradient Descent)을 진행할 시에 **전체 데이터를 사용하는 것 대신 한개 또는 일부 활용**하여 경사하강법을 진행하고 변수를 업데이트한다.

* 전체 데이터로 1번의 업데이트를 하지 않기 때문에 연산량이 감소하고, 자원을 효율적으로 사용 할 수있다.
* 하지만, 전체 데이터를 사용하지 않기 때문에 극소값으로 최단 경로로 이동하지 않는다.

<img width="303" alt="image-20210807180804218" src="https://user-images.githubusercontent.com/88299729/130345005-cff0b807-d982-41a2-832b-6adf4e332cee.png">

#### SGD의 장점

1. 경사하강법(Gradient Descent)의 경우

   볼록 함수에서 적절한 **hyperparameter**(학습률와 학습 횟수) 값이 주어졌을 때 수렴한다.

   선형 함수에서 L2-Norm 으로 구하는 목적식의 경우에는 볼록함수이므로 수렴을 보장하지만, 비선형 함수의 경우 볼록하지 않을 수 있다. 이때, 경사하강법(GD)은 수렴을 보장하지 않지만, SGD의 경우에는 **일부의 데이터를 활용하기 때문에 수렴**한다.

   

   * SGD는 일부 데이터를 사용하기 때문에 hyperparameter에서 mini-batch size도 고려해주어야 한다.

   

<img width="227" alt="image-20210807181603137" src="https://user-images.githubusercontent.com/88299729/130345037-62dd4b83-23fb-4b4d-9f00-6cce6333c124.png" style="50%"> <img width="228" alt="image-20210807181647288" src="https://user-images.githubusercontent.com/88299729/130345054-e031d1dc-e4dc-4ede-8f2d-192af8f319fb.png" style="50%">

​             <선형 함수와 비선형 함수에서의 극소값을 구하는 모습>



2. SGD의 경우

   매 step마다 다른 batch에 들어 있는 각각의 데이터를 사용하기 때문에 목적식이 계속 바뀐다.

   목적식이 모양이 계속 바뀌면서, 경사하강법에서는 극소점이던 곳이 mini-batch에서는 극소점이 아닐 수 있다. 이것은 다른 말로 표현하면 **극소점이 아닌 local minimum에서 탈출 할 수 있다**는 말이다. (반대로, **GD**는 목적식이 바뀌지 않으므로 **local minimum 탈출이 불가능**하다.)



<img width="661" alt="image-20210807182431108" src="https://user-images.githubusercontent.com/88299729/130345071-fdfec505-c941-45ec-a9b1-d1d78cc1edb2.png">

<적당한 batch-size를 설정하게 되면 진동량이 적어지고 안정적으로 극소값으로 수렴한다.>