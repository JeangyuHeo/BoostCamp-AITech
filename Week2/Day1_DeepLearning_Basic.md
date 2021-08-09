### Deep Learning Basic

#### AI 기술 포함 관계

![화면 캡처 2021-08-09 102943](C:\Users\82104\Desktop\화면 캡처 2021-08-09 102943.png)



#### 훌륭한 딥러닝 개발자란?

* having **Math skills**  
* having **Implementation skills** 
* **Knowing** a lot of recent **papers**



### Key components of Deep Learning

* Data : 모델이 **학습** 할 수 있는
* model : 데이터를 적합하게 **변형** 할 수 있는
* loss function : 모델의 **성능을** **측정** 할 수 있는
* algorithm : **loss를 최소화** 하기 위한 



### Data

* Classification : 이미지로 분류하는 것

- Semantic Segmentation : 인공지능이 이미지에 있는 객체를 픽셀 단위로 분류하는 것
- Detection : 물체에 대해서 bounding box를 취해주는 것
- Pose Estimation : 사람의 포즈를 측정해주는 것
- Visual QnA : 보이는 것에 대해서 답변해주는 것



### Model

* AlexNet 
* GoogLeNet 
* ResNet 
* DenseNet 
* LSTM 
* DeepAutoEncoders 
* GAN



### Loss Function

![화면 캡처 2021-08-09 104616](https://user-images.githubusercontent.com/88299729/128721726-b36e796c-b109-4d41-b6a8-bae283a14385.png)



### Historical Review

source -  'Deep Learning's Most Important Ideas - A Brief Historical Review'



* 2012

  AlexNet : 딥러닝이 성능을 발휘하기 시작

  

* 2013

  DQN(Reinforcement learning) : 알파고(Deep Mind) 의 근간이 되었다.

  

* 2014

  Encoder / Decoder : 

  Sequence data(Chinese language sequence) => Encoding => decoding => Sequence data(other language sequence) - language translation에 큰 기여를 하였다.

  

* 2014

  Adam Optimizer : 개인이 사용하여도 결과가 잘 나와서 범용성이 뛰어나다.

  

* 2015

  GAN(Generative Adversarial Network) : Generator, Discriminator 2개를 만들어 학습을 시키는 구조 - 술을 먹다가 발견해 낸 모델

  

* 2015

  Residual Networks : 네트워크 깊이를 늘려준 논문 (ex) 20이 한계였다면 100까지 깊게)

  

* 2017

  Transformer : 나왔을 당시에는 크게 사용되지 않았지만, 성능이 뛰어나 오늘 날에는 RNN은 거의 대체가 되었고 CNN의 자리까지 넘보고 있다.

  

* 2018

  BERT : 다양한 말뭉치, 큰 말뭉치로 학습한 후 fine tuning을 함



* 2019

  GPT-3 : 효과적이나 parameters가 너무 많아 개인이 사용하기에는 어려움



* 2020

  Self Supervised Learning : Label 없는 온라인의 데이터 활용



### Neural Networks & Multi-Layer Perceptron



![image-20210809221019504](https://user-images.githubusercontent.com/88299729/128721820-997d9916-f5fa-49f8-a670-812f6e844480.png)



#### 새처럼 하늘을 날기 위해 꼭 새처럼 생길 필요는 없다. 

이와 같이, 뇌를 모방하고 싶다고 꼭 뇌처럼 동작 할 필요는 없다.   **-최성준 교수님-**



### Linear Neural Network

* **기본 구조**

![화면 캡처 2021-08-09 131854](https://user-images.githubusercontent.com/88299729/128721882-9a9dc564-15c6-42e0-92ff-7632e7c60515.png)



* **가장 최적의 parameters 찾는 과정**

![image-20210809223622061](https://user-images.githubusercontent.com/88299729/128721937-7afe217e-e417-4376-b163-321186ccf7cb.png)![image-20210809223459155](https://user-images.githubusercontent.com/88299729/128722030-7a7711ab-3d11-4e7c-b38c-478391c7bc9a.png)



loss 를 w에 대해서 미분하여 w 값을 업데이트 해주고, b에 대해서 미분하여 b 값을 업데이트 해준다.



![화면 캡처 2021-08-09 131657](https://user-images.githubusercontent.com/88299729/128722091-6e38597f-4b27-4a3c-a4f0-7689b5608925.png)



* **여러 층을 쌓게 되면 어떻게 될까??**



![image-20210809224139653](https://user-images.githubusercontent.com/88299729/128722158-deb62482-6338-4d7a-8d8f-03869363ed9a.png)



선형성을 없애지 않는다면 함수를 f(g(x)) 하는 것에 불과하다.



![image-20210809224228375](https://user-images.githubusercontent.com/88299729/128722203-2ade571d-4f5a-4e07-972b-6b2d563419aa.png)

비선형 변형을 줌으로서 더 적합한 parameter 값으로 수렴 할 수 있다.



* Activation Functions



![image-20210809224356827](https://user-images.githubusercontent.com/88299729/128722247-5cca2ced-4d7b-4750-a895-78ad4f005588.png)



가장 많이 쓰이는 것은 있지만 **정답인 함수는 없다.** 상황에 따라 사용해야 할 함수가 다르다.

가장 많이 쓰이는 것은 ReLU 이다.



* Multi-Layer Perceptron



![image-20210809224525625](https://user-images.githubusercontent.com/88299729/128722293-6ba33511-c0ca-43a0-97ce-8d6975b70e54.png)

위의 과정을 반복해주면 그것이 Multi-Layer Perceptron 이다.