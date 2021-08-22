### Convolution Neural Network (CNN)

#### 고정된 크기의 커널을 움직여가며 연산을 한다.



#### Convolution이란?

**커널을 이용**해 국소적으로 **증폭 또는 감소시켜서 데이터를 추출 또는 필터링** 하는 기법



#### CNN의 Convolution

실제 신호 처리에서 사용되는 convolution이 아닌 **Cross-correlation 기법**이 사용되지만, 통상적으로 Convolution Neural Network라고 불린다.



#### 연산 시 입력, 출력 사이즈

O<sub>H</sub> = H - K<sub>H</sub> + 1

O<sub>W</sub> = W - K<sub>W</sub> + 1



Ex) image(28 x 28), kernel(3 x 3) => output(26 x 26)



* 연산 과정에서 output 채널 수를 늘리고 싶으면 커널의 개수를 늘려야 한다.

* Convolution 연산은 커널이 모든 입력 데이터에 공통적으로 적용되기 때문에 역전파를 계산할때도 Convolution 연산이 나온다.



### Recurrent Neural Network

시간에 의존적(Time-Series data)이거나 순차적인 데이터(Sequence data)를 다루는 데 사용되는 모델



#### Sequence data

순차적으로 들어오는 데이터를 뜻한다. 소리, 문자열, 주가, 영상 자료 등이 있다.

* Sequence data의 경우 **이벤트의 발생 순서가 굉장히 중요**하다. 임의로 데이터를 가공할 경우 원하는 결과물을 얻기 힘들다. 다른 말로 표현하면 **독립동등분포를 위배**하기 쉽다.

* 이를 수학적으로 생각을 해보면, P(X<sub>t+1</sub>) 는 P(X<sub>1</sub>)부터 P(X<sub>t</sub>)까지 순차적으로 조건부 확률을 곱하는 식으로 나타낼 수 있다.

  <img width="660" alt="image-20210808193617420" src="https://user-images.githubusercontent.com/88299729/130345360-38f56922-2a6b-41e1-add2-074c5d4878d5.png">



#### 데이터를 선택하는 방법

1. 직전 데이터 X<sub>t</sub> 부터 설정한 t개만큼의 데이터만 추출해서 사용 (너무 옛날 데이터가 필요 없는 경우)
2. 직전 데이터 X<sub>t</sub> 만 빼고 처음부터 X<sub>t-1</sub> 까지 사용



#### RNN에서의 역전파(BackPropagation)



**BPTT** 

 연산이 다 끝나고 맨 마지막부터 타고타고 오는 방식의 역전파

* 모든 부분에서 진행 시 미분 값이 엄청 커지거나, 작아져서 학습이 불안정해질 수도 있다.
* Gradient Vanishing이 일어날 수 있다. grad가 0이 되면 과거의 정보가 유실 될 수 있다.



**Truncated BPTT**

BPTT의 문제를 해결하기 위해 RNN을 여러 개의 큰 덩어리로 나누어서 각각 BPTT를 진행해준다.