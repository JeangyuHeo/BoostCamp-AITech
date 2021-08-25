## Model

일반적으로 모델이란 대상, 인물, 시스템에 대한 정보를 표현하는 것이고, 인공지능에서는 data set을 통해 원하는 출력을 만들어주는 단계이다.



![화면 캡처 2021-08-25 142349](https://user-images.githubusercontent.com/88299729/130732579-9d264c28-db41-48a1-9227-4077b60338ad.png)



#### Pytorch

Low-level, Pythonic, Flexibility



![화면 캡처 2021-08-25 142450](https://user-images.githubusercontent.com/88299729/130732604-4812546c-6aec-4fbd-9b44-d83bb7c7e134.png)



안의 내용을 더 쉽게 이해하고 고칠 수 있기 때문에 활용적인 측면이 더 뛰어나다.



#### nn.Module

각각의 하위 모듈들이 똑같이 nn.Module을 상속 받고 있고, 같은 메서드를 포함하고 있으므로 상위 모듈인 '내가 생성한 모듈' 에서 메서드를 정의하고 실행시키면 하위 모듈들도 일괄적으로 모두 실행이 된다.



#### state_dict() or list(a.parameters())

이 메서드를 통해 모델에 정의 되어 있는 parameter 목록을 볼 수 있다.



#### data, grad, required_grad

* grad : 업데이트 되는 gradient 값을 보여준다.

* required_grad : 이 param가 back prop을 진행 할지 한할지를 선택한다.
* data : param 값 자체이다.





## Pretrained Model

좋은 품질, 대용량의 데이터로 미리 학습한 모델을 내 목적에 맞게 다듬어서 사용하는 것을 의미한다.



* TorchVision 모델
* timm 모델



#### Code Check

* 가져와서 쓰려는 모델과 내가 학습시키려는 데이터의 유사성을 판단한다.

  * **유사성이 높다**면, 모델 학습은 **Freeze**, 마지막 분류 부분만 **train** 하여 **특징 추출(Feature Extraction)**을 진행한다.

  * 유사성이 **낮다면**, 모델 학습을 **Train**하며, 마지막 분류까지 하여 **미세 조정(Fine tuning)**을 진행한다.

    

    ![화면 캡처 2021-08-25 145214](https://user-images.githubusercontent.com/88299729/130734066-fe0774c7-52bb-47a0-8b0a-837eeec1c059.png)

* 내가 가지고 있는 데이터의 양이 충분한지 판단한다.

  

![화면 캡처 2021-08-25 145232](https://user-images.githubusercontent.com/88299729/130734102-5e1d8a8b-e6da-499d-b94a-5309e889aa9f.png)



#### ImageNET

ImageNET이 발달함에 따라서 CNN은 엄청난 속도로 발전했다.

![화면 캡처 2021-08-25 144535](https://user-images.githubusercontent.com/88299729/130734041-546d96db-eb30-4f5b-8b83-64e608dab0e6.png)