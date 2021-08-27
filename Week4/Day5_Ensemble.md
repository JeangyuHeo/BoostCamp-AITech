## Ensemble

더 나은 성능을 내기 위해서 여러 학습 모델을 사용하는 것



![화면 캡처 2021-08-27 143751](https://user-images.githubusercontent.com/88299729/131079288-a53b7262-97f5-4007-8866-30b5317e848e.png)



#### Hard Voting

그냥 과반의 수가 나온 정답 레이블을 선택한다.



#### Soft Voting

점수의 총합이 가장 높은 정답 레이블을 선택한다.



## Cross Validation

![화면 캡처 2021-08-27 143834](https://user-images.githubusercontent.com/88299729/131079308-61243c6a-0e91-4424-b003-6a34e8e7c6e0.png)



train data의 **일부를 쪼개어 validation set**으로 사용한다. **K개로 쪼갠 후에 각각을 번갈아가면서 validation set으로 사용하는 것을 K-Fold Cross Validation** 이라고 한다.



![화면 캡처 2021-08-27 143954](https://user-images.githubusercontent.com/88299729/131079334-08211b0c-e498-498e-afdd-2a2b6fbbc655.png)



## HyperParameter

시스템의 매커니즘에 영향을 주는 주요한 파라미터이다. 하지만, 모델이 조금만 변화하여도 다시 조정해주어야 하고, 맞추는 데에도 엄청난 시간과 자원이 필요하여 요즘에는 최적화는 안하는 편이다.



#### Optuna

![화면 캡처 2021-08-27 144526](https://user-images.githubusercontent.com/88299729/131079358-3c565859-85db-4d35-9601-3077bd23b23a.png)

파라미터 범위를 주고 그 범위 안에서 trials 만큼 실행하며 hyper parameter 튜닝을 해주는 모듈이다.





## Training Visualization

학습 과정을 기록하고 트래킹 하는 것도 굉장히 중요하다.

 아래의 2개는 이를 도와주는 프로그램들이다.

#### Tensorboard

<img src="https://user-images.githubusercontent.com/88299729/131079375-ba51c700-b52c-4b1f-9555-97afba2973f0.png" alt="화면 캡처 2021-08-27 145357" style="zoom:75%;" /> <img src="https://user-images.githubusercontent.com/88299729/131079406-2b44823b-d27f-44c6-a680-0e921f7f59b5.png" alt="화면 캡처 2021-08-27 145455" style="zoom:75%;" />

#### WandB

![화면 캡처 2021-08-27 145516](https://user-images.githubusercontent.com/88299729/131079495-963d8743-2a08-43eb-8c5e-f01157c34739.png)



### Jupyter notebook

1. 코드를 빠르게 cell 단위로 실행시켜볼 수 있다.

2. EDA 할때 사용하면 굉장히 편리하다.

3. 학습 도중 노트북 창이 꺼지면 돌이킬 수 없다.

   

### python IDLE

1. 구현은 한번만, 사용은 언제든, 코드 재사용이 편리하다.
2. 디버깅을 사용 할 줄 알면, 어떤 코드도 무섭지 않게 된다.
3. 자유로운 실험 핸들링이 가능하다.



### Paper with Codes

최신 논문과 그 코드까지 확인 할 수 있는 사이트이다.



