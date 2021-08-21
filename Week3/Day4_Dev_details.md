## Multi_GPU 학습

이전에는 데이터가 많지 않았지만, 오늘날의 딥러닝은 좋은 GPU로 엄청난 데이터를 학습시켜 좋은 모델을 얻는다.



* Single vs. Multi

  GPU가 1개 vs GPU가 여러개

  

* GPU vs. Node

  GPU를 사용 vs 컴퓨터를 사용

  

* Single Node Single GPU

  1대의 컴퓨터에 1개의 GPU 사용

  

* Single Node Multi GPU

  1대의 컴퓨터에 여러 개의 GPU 사용



* Multi Node Multi GPU

  여러 대의 컴퓨터에 여러개의 GPU 사용



### 모델 병렬화 (Model Parallel)

![화면 캡처 2021-08-21 222602](https://user-images.githubusercontent.com/88299729/130323379-5aeca6f5-c187-40f3-b943-2aba2cdaa783.png)

* 다중 GPU에 학습을 분산하는 두 가지 방법 모델을 나누기 / 데이터를 나누기 
* 모델을 나누는 것은 생각보다 예전부터 썼음 (alexnet) 
* 모델의 병목, 파이프라인의 어려움 등으로 인해 모델 병렬화는 고난이도 과제



![화면 캡처 2021-08-21 222620](https://user-images.githubusercontent.com/88299729/130323391-342c39c4-a205-4b0f-87e8-0fb513cbe6b3.png)



#### Data Parallel

![화면 캡처 2021-08-21 222718](https://user-images.githubusercontent.com/88299729/130323397-c35439bc-005c-4e87-afaa-89be0674098c.png)

*  데이터를 나눠 GPU에 할당후 결과의 평균을 취하는 방법 
* minibatch 수식과 유사한데 한번에 여러 GPU에서 수행



**Data Parallel 종류**

* DataParallel

  ![화면 캡처 2021-08-21 222927](https://user-images.githubusercontent.com/88299729/130323408-13ad629e-6205-4345-98e3-cd4b8618b200.png)

  단순히 데이터를 분배한후 평균을 취함 → GPU 사용 불균형 문제 발생, Batch 사이즈 감소 (한 GPU가 병목), GIL

  

* DistributedDataParallel 

  ![화면 캡처 2021-08-21 222952](https://user-images.githubusercontent.com/88299729/130323413-4a941f9e-bb16-4d3e-bfe8-6990962d3615.png)

  각 CPU마다 process 생성하여 개별 GPU에 할당 → 기본적으로 DataParallel로 하나 개별적으로 연산의 평균을 냄

  참고 : pin_meomory는 메모리에 바로 데이터를 올릴 수 있게 해주는 변수

  ![화면 캡처 2021-08-21 223109](https://user-images.githubusercontent.com/88299729/130323418-7de94993-847f-4d2f-a0ca-9009f8c37525.png)



## Hyperparameter Tuning

* 모델 스스로 학습하지 않는 값은 사람이 지정 (learning rate, 모델의 크기, optimizer 등) 
* 하이퍼 파라메터에 의해서 값의 크게 좌우 될 때도 있음 (요즘은 그닥?) 
* 마지막 0.01을 쥐어짜야 할 때 도전해볼만!



#### 그래프와 같이 은근히 차이가 심하다.

![화면 캡처 2021-08-21 223627](https://user-images.githubusercontent.com/88299729/130323634-b6e7814e-de33-41ab-bd93-15930085c7c7.png)



### Layout

![화면 캡처 2021-08-21 223649](https://user-images.githubusercontent.com/88299729/130323666-9bb64b3b-fa6d-4a84-be67-4e2a86353d3e.png)

Random Layout으로 대략적인 학습이 잘되는 구간을 구하고, Grid Layout을 통해 정확한 값을 수렴시킨다.

1. Grid Layout

   Grid Layout : log의 배수? 형태로 일정 간격으로 파라미터 값을 정한다.

2. Random Layout 

   랜덤으로 값을 설정하고 결과를 확인하며 파라미터 값을 정한다.



### Ray 

![화면 캡처 2021-08-21 224151](https://user-images.githubusercontent.com/88299729/130323673-41913235-e6b1-4510-80b0-a543c09a4883.png)



* multi-node multi processing 지원 모듈 
* ML/DL의 병렬 처리를 위해 개발된 모듈
* 기본적으로 현재의 분산병렬 ML/DL 모듈의 표준 
* Hyperparameter Search를 위한 다양한 모듈 제공



## PyTorch Troubleshooting



### 공포의 단어 : OOM (Out Of Memory)



#### 왜 공포의 단어일까?

* 왜 발생했는지 알기 어려움 
* 어디서 발생했는지 알기 어려움 
* Error backtracking 이 이상한데로 감 
* 메모리의 이전상황의 파악이 어려움



#### 가장 기본적인 해결법

![화면 캡처 2021-08-21 230033](https://user-images.githubusercontent.com/88299729/130324441-55b40dd1-2ebe-4b61-b53e-89ba51a1bbd8.png)

#### 그 외에 다른 해결법

1. GPUUtil

   nvidia-smi 처럼 GPU의 상태를 보여주는 모듈 

   Colab은 환경에서 GPU 상태 보여주기 편함

   

2.  torch.cuda.empty_cache()

   사용되지 않은 GPU상 cache를 정리 

   가용 메모리를 확보 

   del 과는 구분이 필요



3. training loop에 tensor로 축적되는 변수를 확인해보기

   tensor로 처리된 변수는 GPU 상에 메모리 사용

   해당 변수 loop 안에 연산에 있을 때 GPU에 computational graph를 생성(메모리 잠식)



4. del 명령어 적절히 사용하기

   크기가 큰 파라미터를 함부러 복사하지말기



5. 학습시 OOM 이 발생했다면 batch 사이즈를 1로 해서 실험해보기



6. torch.no_grad()

   Inference 시점에서는 torch.no_grad() 구문을 사용 

   backward pass 으로 인해 쌓이는 메모리에서 자유로움
