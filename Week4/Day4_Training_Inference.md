## Training



### 학습에 필요한 요소

#### 1. Loss

output과 target 사이의 차이를 의미한다. 이를 이용하여 gradient를 구해서 param 값들을 업데이트해준다.

* backward()

  이 메서드를 실행하게 되면 requires_grad 값이 True인 param 값들의 grad를 업데이트해준다.



특별한 Loss function

1. Focal Loss 

   Class Imbalance 문제가 있는 경우, 맞춘 확률이 높은 Class는 조금의 loss를, 맞춘 확률이 낮은 Class는 Loss를 훨씬 높게 부여한다.

2. Label Smoothing Loss 

   Class target label을 Onehot 표현으로 사용하기 보다는 ex)[0,1,0,0,0,…] 조금 Soft하게 표현해서 일반화 성능을 높이기 위함 ex) [0.025, 0.9, 0.025, 0.025, …]



#### 2. Optimizer

Learning Rate Scheduler

1. StepLR : step size를 기점으로 lr 값을 낮춰준다.

   ![화면 캡처 2021-08-26 150440](https://user-images.githubusercontent.com/88299729/130909692-5696d0b5-538d-4b0a-90ff-f8c648e74069.png)

2. CosineAnnealingLR  : Cosine 함수 형태처럼 LR을 급격하게 변경시킨다.

   ![화면 캡처 2021-08-26 150429](https://user-images.githubusercontent.com/88299729/130909678-89c36162-abb6-42e8-a128-64539ed364d0.png)

3. ReduceLROnPlateau : 더 이상 성능 향상이 없을 때 LR을 감소시킨다. 대체로 많이 사용된다.

![화면 캡처 2021-08-26 150419](https://user-images.githubusercontent.com/88299729/130909665-d7873458-fad1-4919-a2a9-0d71bdadd59e.png)



#### 3. Metric



![화면 캡처 2021-08-26 150405](https://user-images.githubusercontent.com/88299729/130909642-085440ca-9cb3-4ad2-b1e4-314c94d8c7d9.png)



학습에 직접적으로 사용되는 것은 아니지만, 학습된 모델을 객관적으로 평가할 수 있는 지표가 필요할 때 사용된다.



![화면 캡처 2021-08-26 150501](https://user-images.githubusercontent.com/88299729/130909720-4b88736b-ba6d-4fb7-b232-10a13a05a59e.png)



이때, Accuracy가 높다고해서 좋은 것은 아니고 class 별로 밸런스가 적절히 분포 되어 있어야 하고, 각각의 클래스 별로 성능이 좋아야 한다.





## Train Process



### model.train()

모델에는 train 모드와 evaluation 모드 2가지가 존재하고, 각각 사용되어야 하는 것과 사용되면 안되는 것들을 on/off 해주는 역할을 한다. 이 함수는 모델을 train 할 수 있는 상태로 변경해준다. 



#### optimizer.zero_grad()

![화면 캡처 2021-08-26 151250](https://user-images.githubusercontent.com/88299729/130912427-b8d50273-e66d-4861-86a1-0af7bc1889cf.png)

현재 params에 있는 계산되어 있는 grad 값을 전부 초기화 해준다.



#### loss = criterion(outputs, labels)

![화면 캡처 2021-08-26 151445](https://user-images.githubusercontent.com/88299729/130912471-d90e2021-109e-42ce-9606-21bf9152ec29.png)

지금 params 값을 기준으로 모델의 예측 값과 정답을 비교하여 그 차이인 loss를 구한다. 그 후, backward()를 사용하여 각각에 param에 대한 grad 값을 구하게 된다.



![화면 캡처 2021-08-26 152336](https://user-images.githubusercontent.com/88299729/130912490-9961cdad-1fa9-4c6f-b6c9-3a5999067422.png)



#### optimizer.step()

![화면 캡처 2021-08-26 152427](https://user-images.githubusercontent.com/88299729/130912531-9f38115b-5fc5-4033-983c-c6c1a4b5b74c.png)

back prop을 통해서 구해진 grad 값을 param data 값에 적용시켜준다.



## Inference Process



### model.eval()

이 함수는 모델을 evaluation 할 수 있는 상태로 변경해준다.



#### with torch.no_grad()

평가를 하는 중간에 param 값이 변화해서는 안된다. 모든 param 들에 대해서 requires_grad 값을 False로 만들어주는 함수이다.



#### 성능이 좋은 것들을 저장해둘 수 있다.



![화면 캡처 2021-08-26 152807](https://user-images.githubusercontent.com/88299729/130912560-efcd41fe-f65b-4a28-a753-7d2341a9a67e.png)



#### PyTorch Lightning

![화면 캡처 2021-08-26 152957](https://user-images.githubusercontent.com/88299729/130912580-5b66daf8-16b3-4731-9b9b-73d5f420669f.png)

생산성을 올리기 위해 Keras처럼 만들어진 모듈이다. 굉장히 편리하고 간편하지만, pytorch에 대한 충분한 이해가 바탕이 되지 않은 상태에서는 오히려 독이 될 수 있으니 공부 단계에서는 피하는게 좋다.

