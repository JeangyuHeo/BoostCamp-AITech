## Generative Model

<img width="563" alt="스크린샷 2021-08-14 오후 5 32 33" src="https://user-images.githubusercontent.com/88299729/129440396-592d3c3c-4d1f-421a-a876-5f628621d0a7.png">

학습된 것과 비슷한 이미지를 만드는 것

어떤 이미지가 들어왔을 때 확률 값 하나가 나와서 비슷한지 확인한다. (explicit model)



* **용어 정리**

implicit Model : generation만 가능한 모델

explicit Model : generation과 유사도 확률 계산이 가능한 모델



* 기초가 되는 확률, 통계

<img width="396" alt="스크린샷 2021-08-14 오후 5 32 57" src="https://user-images.githubusercontent.com/88299729/129440410-0398672e-043c-4d7e-9ac6-ef5cbe31fa68.png">



이미지에서 각각의 픽셀이 dependent, independent 하다면?

**모든 픽셀이 dependency**가 있다고 가정을 하면,

**param 의 개수는 2<sup>n</sup>-1** 이고,

**모든 픽셀이 independent** 하다고 가정 한다면,

**param 의 개수는 n**개이다.



하지만, 모든 픽셀이 independent하다는 것은 말이 안된다.



#### Conditional Independence

위의 두 경우의 타협점을 찾은 모델링 기법



* 동작 기반의 3가지 법칙

  <img width="551" alt="스크린샷 2021-08-14 오후 5 33 19" src="https://user-images.githubusercontent.com/88299729/129440437-d31b96df-729c-4c91-82b6-14d625ee1411.png">

  1. Chain rule(연쇄 법칙)

  2. Bayes' rule(베이즈 정리)

  3. 조건부 독립

     <img width="391" alt="스크린샷 2021-08-14 오후 5 33 37" src="https://user-images.githubusercontent.com/88299729/129440449-01f24586-92b7-4520-a6e4-8c4775e5606e.png">

     z가 주어졌을때 x, y는 indepedent하다는 것



#### Auto regressive Model

하나의 정보가 이전 정보들에 dependent 한 모델이다.

* 몇개나 dependent 하냐에 따라서 AR-1 model, AR-N model로 나뉜다.



#### NADE (Neural Autoregressive Density Estimator)

<img width="530" alt="스크린샷 2021-08-14 오후 5 35 33" src="https://user-images.githubusercontent.com/88299729/129440459-dc1f9ab9-2353-4703-a512-c544892e99ef.png">

*i*번째 픽셀 x<sub>i</sub>는 **그 이전까지의 모든 픽셀들에 대해 dependant**하다. 픽셀의 순서가 뒤로 갈수록 받는 입력 x<sub>1:i-1</sub>의 수가 많아지므로, **weight의 길이가 가변적**이다. 이외에는 AR model가 동일하다.



#### Pixel RNN

<img width="454" alt="스크린샷 2021-08-14 오후 5 36 37" src="https://user-images.githubusercontent.com/88299729/129440470-726fe59d-56fd-47d3-ab04-3b84fdfc087f.png">

픽셀을 만들고 싶다!

앞에서 봤던 **auto regressive model 같은 경우에는 fully connected layer**를 통해서 i0 ~ in-1까지의 픽셀을 전부다 고려 할 수 있는 모델을 만들었다면 **RNN을 통해서 만들었다.**



ordering을 어떻게 하느냐에 따라서 row LSTM, diagonal BiLSTM



### Variational Auto Encoder



**posterior distribution** 

 나의 observation이 주어졌을 때, 내가 관심 있어하는 random variable에 대한 확률 분포(z는 latent vector) - 사실 상 구하는 건 불가능하다.

<img width="350" alt="스크린샷 2021-08-14 오후 5 37 00" src="https://user-images.githubusercontent.com/88299729/129440480-b53cbea8-5bdc-41ad-82e0-86536897554a.png">

 **Variational distribution**

posterior distribution은 못구하므로, 학습시키기 위한 근사시킨 분포이다.



그럼 어떻게 구하면 좋을까?

실제 사후분포와의 쿨백 라이블러 발산(KL Divergence)이 최소화되는 varitional distribution을 찾는다.

그런데, 사후분포가 어떤지도 모르면서 사후분포에 근사하는 값을 찾겠다는 것은 어불성설이 아닌가? 그래서 사용하는것이 **ELBO(Evidence Lower BOund) 방법**이다.



<img width="577" alt="스크린샷 2021-08-14 오후 5 37 12" src="https://user-images.githubusercontent.com/88299729/129440483-24e06d36-a388-45db-8758-54e065dc445c.png">


변분추론의 목적은 **사후분포와 variance distribution의 KL divergence를 줄이는 것**이었다. 그런데 사후분포가 무엇인지 모르므로 KL divergence를 어떻게 조작해서 줄여야할 지 모른다.

<img width="232" alt="스크린샷 2021-08-14 오후 5 26 40" src="https://user-images.githubusercontent.com/88299729/129440563-951adf40-4315-4373-9e64-f9bdb150869f.png">



사후분포는 ELBO항과 KL Divergence 항의 합으로 유도할 수 있는데, 이 경우 **KL Divergence를 최소화하기 위해 반대급부로 ELBO 항을 최대화시키는 테크닉이 ELBO법**이다. 이 ELBO항은 구할 수 있으므로(tractable) 이런 방식이 가능하게 된다. 이 기법을 Sandwitch method라고도 부른다.



<img width="476" alt="스크린샷 2021-08-14 오후 5 37 27" src="https://user-images.githubusercontent.com/88299729/129440487-ec6c5ef4-654e-4ee6-8f66-9ae8500bab1a.png">



### GAN (Generative Adversarial Network)

<img width="363" alt="스크린샷 2021-08-14 오후 5 37 56" src="https://user-images.githubusercontent.com/88299729/129440490-99842136-5759-4e46-984e-776da9b05670.png">

A two player minimax game between generator and discriminator.

* **GAN의 장점**
  학습의 결과로 나오는 generator를 학습하는 discriminator가 점차점차 좋아진다.



<img width="564" alt="스크린샷 2021-08-14 오후 5 38 07" src="https://user-images.githubusercontent.com/88299729/129440498-38a5fea2-bf00-411b-b39f-87a815812afc.png">



* **학습 과정**

  1. z라는 잠재분포(latent distribution)에서 출발하여 Generator를 통해 Fake를 만들어낸다.
  2. Discriminator는 기존의 레이블과 Fake 이미지를 비교하여 판독하며 분류기를 학습한다.
  3. Generator는 Discriminator가 Fake 이미지에 대해 True가 나오도록 위조기를 업데이트하여 학습한다.

  

#### DCGAN

<img width="633" alt="스크린샷 2021-08-14 오후 5 40 10" src="https://user-images.githubusercontent.com/88299729/129440503-8bd8a38c-2e8e-4740-a1f6-c65b5d1c05d4.png">



MLP로 기존, 이미지 도메인에서 활용
좋은 테크닉들을 알려줌



#### Info-GAN

<img width="349" alt="스크린샷 2021-08-14 오후 5 40 24" src="https://user-images.githubusercontent.com/88299729/129440509-e86ff91d-0cb4-4efd-a4b9-d931afb4cd57.png">

auxiliary vector를 넣어준다.
generation을 할때 GAN이 특정 모드에 집중 할 수 있게 해준다.

* 특정 모드란? 

  C라고 나오는 원핫 벡터



#### Text2Image

<img width="526" alt="스크린샷 2021-08-14 오후 5 40 34" src="https://user-images.githubusercontent.com/88299729/129440514-a653f9d4-23a0-4aa5-91c7-cc7f695936e5.png">



문장이 주어지면 이미지가 주어진다.



#### Puzzle-GAN

<img width="599" alt="스크린샷 2021-08-14 오후 5 40 42" src="https://user-images.githubusercontent.com/88299729/129440521-ef85b9a6-9023-409a-a83e-a23f8d2202da.png">

이미지 안에 sub-patch가 있어서 얘를 통해서 원래 이미지를 복원하는 GAN



#### CycleGAN 

<img width="517" alt="스크린샷 2021-08-14 오후 5 40 55" src="https://user-images.githubusercontent.com/88299729/129440525-2a0b0ed0-12fc-43fa-9afc-07e81f4b8d4d.png">

이미지 사이의 도메인을 바꿀 수 있는 모델
일반적으로는 똑같은 말이 색만 다른게 필요하지만, cycleGAN 같은 경우에는 필요가 없다.

<img width="608" alt="스크린샷 2021-08-14 오후 5 41 05" src="https://user-images.githubusercontent.com/88299729/129440529-9e1c4284-9587-4280-8700-da35e3b3b9a5.png">



#### Star-GAN

<img width="496" alt="스크린샷 2021-08-14 오후 5 41 13" src="https://user-images.githubusercontent.com/88299729/129440536-7ee06f99-044a-4ebf-ac4e-394d063f1ffb.png">

input이 있고 이를 내가 control 할 수 있는 것



#### Progressive-GAN

<img width="411" alt="스크린샷 2021-08-14 오후 5 41 21" src="https://user-images.githubusercontent.com/88299729/129440549-f1f0e9a7-5705-4377-82e9-b0407c12a41c.png">

저차원부터 고차원 이미지로 늘려나가는 아이디어가 좋았다.

