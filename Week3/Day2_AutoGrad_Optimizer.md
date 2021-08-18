## AutoGrad & Optimizer

![화면 캡처 2021-08-19 014144](https://user-images.githubusercontent.com/88299729/129942907-424563c8-4bc0-4954-a9b7-196766b32560.png)

Layer 는 Block들이 모여서 만들어진다.

그런 Block들은 반복되는 경우가 많다.



#### Torch.nn.Module

![화면 캡처 2021-08-19 014903](https://user-images.githubusercontent.com/88299729/129942938-edb6ebc7-23c7-403c-8e68-d8ca878d6f17.png)

* 딥러닝을 구성하는 Layer의 base class  
* Input, Output, Forward, Backward 정의 
* 학습의 대상이 되는 parameter(tensor) 정의



#### nn.Parameter

* Tensor 객체의 상속 객체  
* nn.Module 내에 attribute가 될 때는 required_grad=True 로 지정되어 학습 대상이 되는 Tensor  
* 우리가 직접 지정할 일은 잘 없음 : 대부분의 layer에는 weights 값들이 지정되어 있음



#### Backward

* Layer에 있는 Parameter들의 미분을 수행  
* Forward의 결과값 (model의 output=예측치)과 실제값간의 차이(loss) 에 대해 미분을 수행 
* 해당 값으로 Parameter 업데이트



![화면 캡처 2021-08-19 021609](https://user-images.githubusercontent.com/88299729/129942970-e1eafc57-edd3-4e05-921a-a1b378052645.png)



## Dataset & Dataloader

![화면 캡처 2021-08-19 021729](https://user-images.githubusercontent.com/88299729/129943494-584cabb5-22b6-460c-a494-67ab8554a29d.png)



#### Dataset Class

* 데이터 입력 형태를 정의하는 클래스 
* 데이터를 입력하는 방식의 표준화 
* Image, Text, Audio 등에 따른 다른 입력 정의

 

#### Dataset 사용 시 유의점

* 데이터 형태에 따라 각 함수를 다르게 정의함 
* 모든 것을 데이터 생성 시점에 처리할 필요는 없음 : image의 Tensor 변화는 학습에 필요한 시점에 변환 
* 데이터 셋에 대한 표준화된 처리방법 제공 필요 → 후속 연구자 또는 동료에게는 빛과 같은 존재 
* 최근에는 HuggingFace등 표준화된 라이브러리 사용



#### Dataloader Class

* Data의 Batch를 생성해주는 클래스 
* 학습직전(GPU feed전) 데이터의 변환을 책임 
* Tensor로 변환 + Batch 처리가 메인 업무 
* 병렬적인 데이터 전처리 코드의 고민 필요



![화면 캡처 2021-08-19 022022](https://user-images.githubusercontent.com/88299729/129943520-6fe28c8a-1137-4931-a7c1-7d7cd6732b96.png)

![화면 캡처 2021-08-19 022030](https://user-images.githubusercontent.com/88299729/129943538-57db0cd8-73a7-4c59-a01d-e2c8ed615a58.png)

