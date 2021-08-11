## Convolution Neural Network

filter의 모양에 따라서 다르게 이미지의 특징을 추출 할 수 있다.

필요한 param의 개수는 필터의 크기 A x A와 input, output의 depth(channel의 수)를 곱한다.



![화면 캡처 2021-08-12 010122](https://user-images.githubusercontent.com/88299729/129065310-e17c431a-5763-474a-9051-bf2c7e299cb8.png)



**the number of param = f<sub>w</sub>  x  f<sub>h</sub>  x  #channel<sub>in</sub>  x  #channel<sub>out</sub>**

 

#### Exercise



![image-20210812010841914](C:\Users\82104\AppData\Roaming\Typora\typora-user-images\image-20210812010841914.png)



#### CNN 레이어 별 역할

CNN : 이미지에서 유용한 정보를 추출한다. (feature extraction)
FC (Fully Connected Layer) : 이미지에 대한 평가를 내린다. (decision making)



* param 숫자가 늘어나면 학습이 어렵고, generalization performance 가 떨어진다. ( overfitting 될 확률이 증가한다.)



#### Stride  

내가 얼마나 dense하게 sparse하게 찍을지 정하는 것



![화면 캡처 2021-08-12 010341](https://user-images.githubusercontent.com/88299729/129064588-7e3b4bfd-b460-40e8-b7d5-b8d199a6f2c1.png)

#### Padding

값을 테두리에 덧대주는 역할을 한다.



![화면 캡처 2021-08-12 010400](https://user-images.githubusercontent.com/88299729/129065070-a4c104cf-fa2c-4652-a0a3-18a7e37526c8.png)



> 왜 dense layer의 parameter 수 많은가?

CNN의 경우, 동일한 커널이 convolution network 의 모든 부분에 동일하게 적용되는 shared parameter를 사용하기 때문에 훨씬 적다.



#### AlexNet



![화면 캡처 2021-08-12 013024](https://user-images.githubusercontent.com/88299729/129067446-032931b5-3b21-4839-89ab-8a134c62d858.png)

>  Alexnet 2개로 나눈 이유 

1개의 GPU 메모리에 들어가는 사이즈에 맞추다 보니까 2개의 모델로 나눴다.



#### VGG

3x3 filter를 사용한 것이 포인트라고 할 수 있다.

![화면 캡처 2021-08-12 013142](https://user-images.githubusercontent.com/88299729/129067801-4c354bd1-5295-4c35-a009-78e9c10ad90d.png)



* WHY?

  filter가 커질수록 receptive field가 커진다.

  receptive field란? 1개의 conv feature map 값을 얻어내기 위해서 고려 할 수 있는 입력의 special dimension



#### GoogLeNet



![화면 캡처 2021-08-12 013255](https://user-images.githubusercontent.com/88299729/129067834-267ee3a8-0be7-4b37-8803-e621074956ae.png)



1x1 conv를 사용함으로서 parameter의 개수를 줄였다.



#### ResNet



![화면 캡처 2021-08-12 013717](https://user-images.githubusercontent.com/88299729/129068841-2ede1f86-1930-4d47-a44f-4986c3d2f0e5.png)



layer가 커지면서 학습이 제대로 되지 않는 문제가 있었다. 이를 해결하기 위해 identity map을 사용했다.

* identity map

Neural network 출력 값에 x(입력 값)을 더해준다.

이 과정에서 차이(residual)만큼만 학습을 하게 된다.

input과 output의 차원을 맞춰주기 위해서 1x1 conv을 사용하기도 한다.



#### DenseNet



![화면 캡처 2021-08-12 014118](https://user-images.githubusercontent.com/88299729/129069019-c546b3ba-27b1-4832-bf4e-0adae262c27c.png)

ResNet과 아이디어는 같지만 더해주지 않고, Neural network 출력 값과 x(입력 값) 따로 가져간다.

* 깊어질수록 데이터가 많아져서 중간중간 1x1 conv를 이용해 줄여줘야 한다. 





#### 요약



![화면 캡처 2021-08-12 014327](https://user-images.githubusercontent.com/88299729/129069321-2124249c-1866-47bb-bf51-9e361391a359.png)



## Semantic Segmentation

어떤 이미지를 픽셀마다 분류 하는 것

![화면 캡처 2021-08-12 021253](https://user-images.githubusercontent.com/88299729/129073987-0aee4693-c353-40de-b2b7-8210cf3f64d0.png)



#### Fully Convolutional Network

<img src="https://user-images.githubusercontent.com/88299729/129074003-13c873e0-12f6-4e03-9c57-d197cffdbf1c.png" alt="화면 캡처 2021-08-12 021336" style="zoom:75%;" /><img src="https://user-images.githubusercontent.com/88299729/129074057-da187e62-a92c-498e-a7e1-79c323a406fc.png" alt="화면 캡처 2021-08-12 021325" style="zoom:75%;" />



Dense layer를 없애기 위한 기본이 되는 테크닉이다. (convolutionization)

1. input image에 상관없이 network 가 돌아간다.
2. dense layer를 사용하지 않을 수 있다.
3. parameter 수는 Dense layer와 같다.
4. output이 커지게 되면 그거에 비례해서 뒷단의 special dimension이 커진다.



![화면 캡처 2021-08-12 021358](https://user-images.githubusercontent.com/88299729/129074119-88ab2d91-a691-433d-9a72-a8a494df1992.png)



#### Deconvolution (Convolution Transpose)



![화면 캡처 2021-08-12 021423](https://user-images.githubusercontent.com/88299729/129074166-49adc16a-bf29-478a-93fb-0ead526dbd7b.png)



* special dimension을 키워준다.
* Convolution의 진짜 역연산은 아니지만 파라미터의 수나 입력 출력의 느낌으로 봤을 때는 똑같다.





## Detection

Bounding box를 취해주는 것



#### R-CNN

![화면 캡처 2021-08-12 021445](https://user-images.githubusercontent.com/88299729/129074209-ffc42151-c6f4-47de-9db5-b7b977ecb672.png)



1. 2000개 정도의 영역을 정한다.
2. alexnet으로 영역 별 특징 추출한다.
3. 각 영역을 svm으로 분류한다.



#### SPPNet

![화면 캡처 2021-08-12 021505](https://user-images.githubusercontent.com/88299729/129074322-5d190ecc-b116-47a1-94a9-34966597bc66.png)



1. 이미지 전체에 대해서 1번의 conv feature맵을 만든다.
2. 뽑힌 바운딩 박스의 conv feature맵의 텐서만 긁어오자



#### Fast R-CNN

![화면 캡처 2021-08-12 021520](https://user-images.githubusercontent.com/88299729/129074443-e2c356db-1c82-410e-8f7b-dcd035a4b677.png)

1. 이미지 2000개 뽑는다.
2. feature맵 이미지 전체에 대해서 한번만 만든다.
3. output 쪽 ROI feature vector를 사용해 classification와 바운딩 박스 regression를 처리했다.



#### Faster R-CNN
바운딩 박스 뽑는 것도 network를 쓰자는 아이디어에서 시작되었고, 이를 Region Proposal Network(RPN)이라고 부른다.



* RPN 

  ![화면 캡처 2021-08-12 021541](https://user-images.githubusercontent.com/88299729/129074503-01e97eee-ddd8-4d07-babc-a4c7fde2343b.png)



* 어떤 크기의 물체들이 있을지 알고 있는 것
  templete를 만들어 놓고 이것들이 얼마나 바뀔지에 찾는다.



![화면 캡처 2021-08-12 021557](https://user-images.githubusercontent.com/88299729/129074565-41e2fccb-8fa4-4242-8715-88faae2961a2.png)

* Fully Conv
  모든 영역을 돌면서 찍는다.
  물체가 들어 있을지 없을지 들고있다.
  1. 9 개의 box 박스 사이즈를 가지고 있다.
  2. 4 개의 늘리고 줄이는 방식을 가지고 있다.
  3. 2 개의 사용 가능한 box인지 classification 것을 가지고 있다.



![화면 캡처 2021-08-12 021619](https://user-images.githubusercontent.com/88299729/129074665-f1460b2a-241d-4af8-994a-f2c08ff81178.png)

#### YOLO

![화면 캡처 2021-08-12 022618](https://user-images.githubusercontent.com/88299729/129075232-385458c2-0538-402d-9262-288908988b80.png)

Faster보다 빠르다.
여기서는 bounding 박스를 분류하는 과정이 없이 한번에 한다.



1. 이미지를 grid cell로 나눈다.
2. 이미지 안에 내가 찾고 싶은 물체 중앙이 그리드 안에 들어가는지 체크한다.
3.  해당 그리드 셀이 해당 물체에 대한 bounding와 Classification을 같이 예측해준다.

