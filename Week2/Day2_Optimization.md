## Optimization



> 여는 글

Language is the source of misunderstanding.

* 잘못된 정의와 개념은 큰 문제를 야기 할 수 있기 때문에 정확하게 이번에 익히자!



#### Gradient Descent

찾고자 하는 parameter를 가지고 lost function을 편미분하고 그 값을 이용하여 학습을 한다. 앞의 과정을 local minima에 도달할 때까지 iterative 하게 한다.

(자세한 것은 경사하강법 정리 참고)



#### Generalization

최소의 training error가 최소의 Test error를 보장하지는 않는다. 즉, **처음 보는 데이터에 대해서 얼마나 잘 작동하는지를 의미한다.**

![화면 캡처 2021-08-10 102310](https://user-images.githubusercontent.com/88299729/128812756-b228a66f-5e17-44b6-9d9e-30edcfb5c0f3.png)

* generalization gap : train error, test error 사이의 갭
* generalization performance가 높으면 네트워크 성능이 학습 데이트와 테스트 데이터가 비슷하게 나올 것이다.



#### Overfitting



![화면 캡처 2021-08-10 102523](https://user-images.githubusercontent.com/88299729/128812775-23d08cb6-9598-461f-b6a8-1ff117793299.png)



Overfitting하게 되면 train data에서는 훌륭한 performance를 보이지만, test data와 같이 처음 보는 데이터에서는 굉장히 안좋은 performance를 보여준다.

* network가 너무 간단하거나 training을 조금시킬 때 일어난다. (하지만 이론적인 말일 뿐 저렇게 overfitting된 모습이 원하는 모델일수도 있기 때문에 잘못된 것은 아닐 수 있다.)



#### Cross-validation (K-fold Validation)



![화면 캡처 2021-08-10 103956](https://user-images.githubusercontent.com/88299729/128815447-8eae23f9-422d-4894-9615-07411f9f41cf.png)



일반적으로 학습 시킬 때, **Train data set**과 **Test data set**을 나누어서 사용한다. 이때, **Test set은 학습시키는 데에는 절대 사용되어서는 안되기** 때문에 **Train data set을 K개로 나누고** 그 중에 **한개를 validation set**으로 사용한다. 

* hyperparameter : 모델 안에서 **내가 정해야 하는 값**들이다.

* train set(**(K-1)-fold**)과 validation set(**1-fold**)을 가지고 hyperparameter를 정한 후에 train set과 validation set을 합쳐서(**K-fold**) 학습을 시킨다.



#### Bias and Variance



![화면 캡처 2021-08-10 104508](https://user-images.githubusercontent.com/88299729/128815569-da8f6d8b-887f-473a-aa48-ed234dcfb9d3.png)



Variance : 입력을 넣었을 때 **출력이 얼마나 일관적**인가? (높으면 overfitting 될 가능성 올라감, 낮으면 일관적)

Bias : 출력들의 mean이 목적에서 얼마나 벗어나는가? (높으면 많이 벗어난 것)



#### Trade-Off



![화면 캡처 2021-08-10 105036](https://user-images.githubusercontent.com/88299729/128815603-e7ae0d25-745f-4bdd-8305-ed7f9577d450.png)



t = target (true target에 noise가 껴있다고 가정한다.)

f^= NN output



라고 했을 때, cost 를 최적화 하는 과정에서 **3가지 부분**으로 나눌 수 있고, **한개를 낮추면 다른게 오르게** 된다.



#### Bootstrapping

전체 데이터를 random sampling을 통해 여러 개의 서로 다른 data set을 만드는 것



#### Bagging vs Boosting

학습 데이터를 여러 개 만들어 (bootstrapping) 학습시킨다. 여러 data set에 대한 output이 나오고, 거기서 평균을 내어 사용한다. 

* 이러한 기법을 'Ensemble(앙상블)' 이라 부른다.
* **1개의 큰 데이터가 더 효과적일 것 같지만** Bagging을 통해 **여러 작은 데이터의 결과물이 효과적**이다.



#### Boosting

sequential 하게 동작하는 모델 형식이다. 

100개의 데이터가 있다고 가정하면, 80, 20개의 데이터로 나누고 80에 대해서 잘 동작하는 모델을 만든다. 하지만, 이는 20개의 데이터에 대해서 동작이 잘 안될 수 있다. 따라서, 20개에 대해서 잘 동작하는 모델을 만든다. 이런 식으로 **작은 데이터에서 잘 동작하는 서로 작은 모델들을 sequential 하게 연결하여 모델**을 만든다.



![화면 캡처 2021-08-10 110856](https://user-images.githubusercontent.com/88299729/128816847-60db03dd-a966-46e4-b601-09630e937697.png)



#### Gradient Descent Methods (1)



<img src="https://user-images.githubusercontent.com/88299729/128817192-ff0249af-d008-4ce6-92d4-980a52a4b1ed.png" alt="화면 캡처 2021-08-10 111103" style="zoom:67%;" />



#### Batch-size Matters



![화면 캡처 2021-08-10 111357](https://user-images.githubusercontent.com/88299729/128817468-cfe5ff2d-a46f-4a78-bc4f-ebf7c88b7820.png)



large batch를 사용하는 경우 sharp Minimum과 같은 모양을 가지는 경향성이 있고, small batch를 사용하는 경우 Flat Minimum과 같은 모양을 가진다. training data와 test data의 그래프가 서로 다르고 거기서 **generalization performance를 고려해봤을 때, small batch를 사용하는 것이 더 좋다.**





### Gradient Descent Methods (2)



#### 1. SGD (Stochastic Gradient Descent)



![화면 캡처 2021-08-10 113319](https://user-images.githubusercontent.com/88299729/128819756-813d1e2e-f7be-48e2-be54-c84fd9bd6560.png)

적합한 Learning rate를 정하는게 어렵다.



#### 2. Momentum



![화면 캡처 2021-08-10 113541](https://user-images.githubusercontent.com/88299729/128864717-2d0d0e5c-c4e3-4c47-9c47-d2eaf25e0f3c.png)

local minimum에 converging 을 잘 못한다.

**흘러가던 방향을 어느정도 유지**하기 때문에 어느정도 왔다갔다해도 어느정도 잘 학습이 잘 된다.



#### 3. NAG (Nesterov Accelerated Gradient)



![화면 캡처 2021-08-10 113735](https://user-images.githubusercontent.com/88299729/128864333-47e297a0-4a87-47bf-89d8-4fe154624675.png)



미리 이번 gradient로 업데이트 될 lost를 미분하여 이번 gradient에 반영한다.



#### 4. Adagrad



![화면 캡처 2021-08-10 114328](https://user-images.githubusercontent.com/88299729/128864386-2458d107-5d85-4dca-94bd-0a9705f92e7d.png)

많이 변한 parameter 들에 대해선 작게 변화시키고, 적게 변한 parameter 들에 대해선 많이 변화시킨다.

*G<sub>t</sub>* : 얼마나 많이 변화왔나를 더해온 것 (점점 커진다)

G가 무한대로 갈수록 업데이트가 멈춰진다.

E(Epsilon) : 0으로 나눠지지 않게 하기 위함.



#### 5. Adadelta



![화면 캡처 2021-08-10 115959](https://user-images.githubusercontent.com/88299729/128864432-682018a1-f3da-4304-bd4b-ed56aa478101.png)



Adagrad의 분모가 과도하게 커지는 것을 방지하기 위해 무작정 더하지 않고, gradient의 가중 평균을 구해준다.

분모가 과도하게 작아지는 것을 방지하기 ㅜ이해 시점 t에서의 기울기 변화를 크게 반영하고 과거의 것은 적게 반영시킨다.



#### 6. RMSprop



![화면 캡처 2021-08-10 120139](https://user-images.githubusercontent.com/88299729/128864816-d72cea4b-dea2-426d-a8c4-550e139f1313.png)



논문이 아닌 Geoff Hinton의 Coursera강연 시간에 제안한 내용이다.

decay rate = 0.9, stepsize는 0.001로 제안했다.



#### 7. Adam



![화면 캡처 2021-08-10 120405](https://user-images.githubusercontent.com/88299729/128864834-77a59d79-1f9c-4d5b-843c-1c8563b46cce.png)



adaptive learning rate과 momentum 방식을 모두 적용시킨 모델로 제일 작동을 잘한다.



### Regularization

Generalization 이 잘되게 하는 여러가지 테크닉들



* Early stopping



![화면 캡처 2021-08-10 121008](https://user-images.githubusercontent.com/88299729/128865125-1d5fca9b-3cd5-4d9b-bab0-37c71e7a721b.png)



말그대로 모델이 overfitting 되어 validation set의 error가 감소하다가 증가하기 시작하면 진행을 멈춘다.



* Parameter norm penalty

파라미터가 너무 커지지 않게 하는 것

파라미터를 다 제곱하고 더하여 나온 숫자를 같이 gradient descent 진행 시에 같이 줄여준다.

-> 파라미터 숫자는 작으면 좋다 (크기 기준에서)



* Data augmentation



![화면 캡처 2021-08-10 214638](https://user-images.githubusercontent.com/88299729/128869201-49039d25-5ecb-448a-8bf9-41121c356545.png)



주어진 데이터를 label 이 변하지 않는 선에서 변행시켜 준다.(돌리거나 뒤집거나 확대하거나 축소한다.)



* Noise robustness



![화면 캡처 2021-08-10 215507](https://user-images.githubusercontent.com/88299729/128870447-a743a68b-958d-4710-9949-bfc590409fc3.png)



noise를 입력과 weight에 추가한다.

이 부분이 왜 잘 동작하는 지는 아직 말이 많다.





* Label smoothing



![화면 캡처 2021-08-10 122659](https://user-images.githubusercontent.com/88299729/128870526-6e4e9504-7be5-4014-a14c-a4c043ded237.png)



2개의 이미지를 뽑아서 섞어준다. 이때, label도 합친 것을 반영하여 바꿔준다.



* Dropout

  ![화면 캡처 2021-08-10 220309](https://user-images.githubusercontent.com/88299729/128871589-5e151b2a-5df3-4626-8eba-afa03c690103.png)

  

random하게 dropout rate 만큼의 node를 각 layer에서 뽑아서 w값을 0으로 만들어준다.

각각의 neuron들이 robust한 feature를 보여주게 된다.



* Batch normalization



![화면 캡처 2021-08-10 220512](https://user-images.githubusercontent.com/88299729/128871915-a5d84470-ae3f-47be-aa61-9e536952b102.png)



각 계층에서 데이터들에 대해서 평균(empirical mean)을 빼주고 분산(variance)으로 나누어줌으로서 정규화를 진행해준다.

