## Introduction to PyTorch



#### PyTorch VS TensorFlow



![화면 캡처 2021-08-18 022503](https://user-images.githubusercontent.com/88299729/129772684-6dac9e3b-5c6f-434c-9e01-3f9e05ba5126.png)



TensorFlow 

* Define and Run : 그래프를 다 그려놓고, 데이터를 동작 시에 넣는다.
* 제품을 만들어내고 출시하는 데에서는 다양한 도구들이 쉽게 연결이 돼서 많이 사용한다.



PyTorch 

* Define by Run : 그래프를 그리면서 데이터를 넣는다.
* 개발 과정에서 디버깅이 쉬워 논문 작성이나 아이디어 구현 시에 많이 사용한다.



![화면 캡처 2021-08-18 022531](https://user-images.githubusercontent.com/88299729/129772716-211ae143-0d5f-44c3-ad6c-8ae87b49dcb1.png)





#### PyTorch Operations

![화면 캡처 2021-08-18 022751](https://user-images.githubusercontent.com/88299729/129772932-c4d392a8-b7fc-4481-8a93-7212f75d5fba.png)



* 다차원 Arrays 를 표현하는 PyTorch 클래스 
* 사실상 numpy의 ndarray와 동일 (그러므로 TensorFlow의 Tensor와도 동일)  
* Tensor를 생성하는 함수도 거의 동일



#### dot VS mm VS matmul



**dot** 

vector, scalar를 연산한다.



**matmul**

matrix multiplication 연산에서 broadcasting 지원한다.



 **mm**

matrix multiplication 연산에서 broadcasting 지원 안한다.



#### AutoGrad

![화면 캡처 2021-08-18 023529](https://user-images.githubusercontent.com/88299729/129774008-7979e6b9-84bd-4346-b739-d0997562156b.png)

PyTorch의 핵심으로서 자동 미분을 의미한다. 이는, chain rule을 이용하여 back propagation에 사용된다.



### Jupyter notebook

#### 장점

초기 단계에서는 대화식 개발 과정이 유리 → 학습과정과 디버깅 등 지속적인 확인



#### 단점

배포 및 공유 단계에서는 notebook 공유의 어려움 → 쉬운 재현의 어려움, 실행순서 꼬임



#### 결론

DL 코드도 하나의 프로그램 : 개발 용이성 확보와 유지보수 향상 필요



#### PyTorch Template

[template1](https://github.com/FrancescoSaverioZuppichini/PyTorch-Deep-Learning-Template)		[template2](https://github.com/PyTorchLightning/deep-learning-project-template)		[template3](https://github.com/victoresque/pytorch-template)



3가지의 Template 예시를 보고 연습하면 좋다. 그 중 가장 괜찮은 것은 3번이다.