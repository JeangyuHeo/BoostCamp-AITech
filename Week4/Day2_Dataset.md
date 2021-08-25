## Dataset

사람들은 딥러닝이라고 하면, 모델을 만들고 학습시키는 것이 대부분을 이룰 것이라고 생각하지만, 실제로는 80%정도가 데이터를 분석하고 필요한 모습으로 바꾸는데 사용된다.



![화면 캡처 2021-08-25 134647](https://user-images.githubusercontent.com/88299729/130730137-76cca996-ed70-48ef-9171-214e2c1afb3c.png)



#### data

1. competition data는 상태가 굉장히 양호한 편이다.
2. 대부분의 데이터는 필요 이상으로 많은 정보를 가지고 있다.
3. 다양한 preprocessing 연산으로 필요한 데이터를 추출해낸다.
4. 연산의 효율을 높이기 위해 Resize 사용을 고려하면 좋다.
5. 밝기를 밝게 만들어주면 데이터에서 특징점을 추출하기 좋아지는 경우가 있다. (ex. 안구 검사)



#### Generalization

train set에서 일정 부분을 validation set으로 분리하여 평가를 실행한다.



#### Data Augmentation

1. 데이터가 가질 수 있는 경우의 수나 될 수 있는 상태들을 생각하며 그 상태와 경우를 추가해주면 성능이 많이 개선 될 수 있다.
2. 문제가 만들어진 배경과 모델의 쓰임새를 살펴보면 힌트를 얻을 수 있다.



## Data Generation

데이터 셋을 잘 만들어도 잘 출력해야 의미가 있다.



#### 좋은 출력

1. 처리 할 수 있을 정도의 데이터만 출력한다.

![화면 캡처 2021-08-25 140526](https://user-images.githubusercontent.com/88299729/130730161-a66bd1e3-4145-4693-8467-ca97ae358af5.png)

2. data set을 효율적으로 사용 할 수 있도록 하는 기능을 사용한다.

![화면 캡처 2021-08-25 140637](https://user-images.githubusercontent.com/88299729/130730193-556d63ba-9ddd-466a-9fa5-450c52a1e1c9.png)



#### Dataset과 DataLoader의 차이점 

* Data set : Vanilla 데이터를 원하는 형태로 출력해주는 클래스
* Data loader : Data set을 더욱 효율적으로 사용하기 위한 클래스

