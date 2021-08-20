## 모델 불러오기

#### MODEL.SAVE()

* 학습의 결과를 저장하기 위한 함수 
* 모델 형태(architecture)와 파라메터를 저장 
* 모델 학습 중간 과정의 저장을 통해 최선의 결과모델을 선택 
* 만들어진 모델을 외부 연구자와 공유하여 학습 재연성 향상



![화면 캡처 2021-08-20 152048](https://user-images.githubusercontent.com/88299729/130190450-56b2c547-627b-4741-99f2-03e1eaaab396.png)



#### Checkpoints

* 학습의 중간 결과를 저장하여 최선의 결과를 선택 
* earlystopping 기법 사용시 이전 학습의 결과물을 저장 
* loss와 metric 값을 지속적으로 확인 저장 
* 일반적으로 epoch, loss, metric을 함께 저장하여 확인 
* colab에서 지속적인 학습을 위해 필요

![화면 캡처 2021-08-20 152211](https://user-images.githubusercontent.com/88299729/130190499-942e8b48-8a5c-41fc-a3d0-423e6fb0b984.png)



#### Pretrained Model Transfer Learning

다른 사람이 만든 모델을 쓰고 싶다!!



* 다른 데이터셋으로 만든 모델을 현재 데이터에 적용 
* 일반적으로 대용량 데이터셋으로 만들어진 모델의 성능 ↑ 
* 현재의 DL에서는 가장 일반적인 학습 기법 
* backbone architecture가 잘 학습된 모델에서 일부분만 변경하여 학습을 수행함



> 다양한 모델들

1. [git repo](https://github.com/rwightman/pytorch-image-models#introduction)
2. [NLP의 표준 model](https://huggingface.co/models)



#### Freezing

![화면 캡처 2021-08-20 153127](https://user-images.githubusercontent.com/88299729/130190539-a09a6a15-cedd-4c5f-8735-36696ba17104.png)



pretrained model을 활용 시 모델의 일부분을 frozen 시키고 내가 값을 얻어야 할 부분만 변경



#### 활용해보기 

![화면 캡처 2021-08-20 153143](https://user-images.githubusercontent.com/88299729/130190574-ffecccfd-345d-4cef-8f53-b6f58af9e229.png)



## Monitoring tools for PyTorch

### 좋은 도구들

print문도 좋지만 데이터들을 보여줄 수 있는 좋은 도구들이 많다.



#### 1. Tensorboard

![화면 캡처 2021-08-20 145001](https://user-images.githubusercontent.com/88299729/130186818-2f7929ec-13d2-4bbf-bcc0-9db80d3b7adc.png)

* TensorFlow의 프로젝트로 만들어진 시각화 도구 
* 학습 그래프, metric, 학습 결과의 시각화 지원 
* PyTorch도 연결 가능 → DL 시각화 핵심 도구



#### 각 기능들

* scalar : metric 등 상수 값의 연속(epoch)을 표시 
* graph : 모델의 computational graph 표시 
* histogram : weight 등 값의 분포를 표현 
* Image : 예측 값과 실제 값을 비교 표시 - mesh : 3d 형태의 데이터를 표현하는 도구



#### 사용 코드

![화면 캡처 2021-08-20 145604](https://user-images.githubusercontent.com/88299729/130186849-9d173a76-2b4b-4861-bdb4-aae327bc6e99.png)



#### 2. Weight & biases

![화면 캡처 2021-08-20 145018](https://user-images.githubusercontent.com/88299729/130186829-e2571f8a-bc84-4f69-8d64-a7ec3a1ac37f.png)

* 머신러닝 실험을 원활히 지원하기 위한 상용도구 
* 협업, code versioning, 실험 결과 기록 등 제공 
* MLOps의 대표적인 툴로 저변 확대 중



#### 사용 코드

![화면 캡처 2021-08-20 145642](https://user-images.githubusercontent.com/88299729/130186889-99847871-c704-4e1d-bd3c-f5e6b38805bd.png)

