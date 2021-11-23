# 모델 경량화 개요

## 경량화

### 경량화의 목적

#### On device AI

![화면 캡처 2021-11-24 012318](https://user-images.githubusercontent.com/88299729/143072848-8d581a0f-ef9d-4eee-b766-e38bf6e4b45a.png)

<br>

#### AI on cloud(or server)

* 배터리, 저장 공간, 연산 능력의 제약은 줄어드나, latency와 throughput의 제약이 존재 
  * latency: 한 요청의 소요 시간
  * throughput: 단위 시간당 처리 가능한 요청 수
* 같은 자원(=돈)으로 더 적은 latency와 더 큰 throughput이 가능하다면?

<br>

#### Computation as a key component of AI progress

![화면 캡처 2021-11-24 012635](https://user-images.githubusercontent.com/88299729/143072875-20608eeb-2a1d-478d-9140-1ee5a4743dd4.png)

* 2012년 이후 큰 AI 모델 학습에 들어가는 연산은 3, 4개월마다 두배로 증가해옴 
* 2012년 기준, 2018년에는 약 300,000x 증가됨 
* (참고)연산 측정 방법
  * 1.Counting operations (FLOPs) 
  * 2.GPU times 
    * [1. VGG16] 
      * 1.2M images x 74 epochs x 16 GFLOPS x 2 add-multiply x 3 backward pass = 8524 PF = 0.098 pfs-day
    * [2. VGG16] 
      * 4 Titan Black GPU’s x 15 days x 5.1 TFLOPS/GPU x 0.33 utilization = 10,000PF = 0.12pfs-days

<br>

#### 경량화는?

* 모델의 연구와는 별개로, 산업에 적용되기 위해서 거쳐야하는 과정
* 요구 조건 (하드웨어 종류, latency 제한, 요구 throughput, 성능)들 간의 trade-off를 고려하여 모델 경량화/최적화를 수행

<br>

### 경량화 분야 소개

#### Efficient arichitecture  design

* 매년 쏟아져 나오는 블록 모듈들
* 각 모듈 블록마다의 특성이 다름(성능, 파라미터 수, 연산 횟수, etc)

![화면 캡처 2021-11-24 014135](https://user-images.githubusercontent.com/88299729/143072915-4fc04bcc-3bcf-42b7-bc26-ac26891adb65.png)

<br>

#### Efficient architecture design; AutoML, Neural Architecture Search

* Software 1.0: 사람이 짜는 모듈 
* Software 2.0: 알고리즘이 찾는 모듈

![화면 캡처 2021-11-24 014254](https://user-images.githubusercontent.com/88299729/143072996-af0ce33c-32c3-401b-8e1f-a1c6a8ab276b.png)

<br>

* 모델을 찾는 네트워크 (controller)

  

![화면 캡처 2021-11-24 014411](https://user-images.githubusercontent.com/88299729/143073015-c2cb6eff-2791-4b8c-b49e-f32e8efab2a0.png)

<br>

* 사람의 직관보다 상회하는 성능의 모듈들을 찾아 낼 수 있음

![화면 캡처 2021-11-24 014453](https://user-images.githubusercontent.com/88299729/143073035-908b6f13-3c96-4515-ab78-3bd9f5d01013.png)

<br>

#### Network Pruning; 찾은 모델 줄이기

* 중요도가 낮은 파라미터를 제거하는 것 
* 좋은 중요도를 정의, 찾는 것이 주요 연구 토픽 중 하나 (e.g. L2norm이 크면, loss gradient 크면, 등등) 
* 크게 structured/unstructured pruning으로 나뉘어짐

![화면 캡처 2021-11-24 014626](https://user-images.githubusercontent.com/88299729/143073060-919d44fd-d6e9-4889-9f0b-0e9500cda5df.png)

<br>

#### Network Pruning; Structured pruning

* 파라미터를 그룹 단위로 pruning하는 기법들을 총칭 (그룹; channel / filter, layer 등)
* Dense computation에 최적화된 소프트웨어 또는 하드웨어에 적합한 기법

![화면 캡처 2021-11-24 014952](https://user-images.githubusercontent.com/88299729/143073094-cde9f358-1373-44a4-a183-e7bab3f07153.png)

<br>

#### Network Pruning; Unstructured pruning

* 파라미터 각각을 독립적으로 pruning하는 기법
* Pruning을 수행할수록 네트워크내부의 행렬이 점차 희소(sparse)해짐
* Structured Pruning과 달리 sparse computation에 최적화된 소프트웨어 또는 하드웨어에 적합한 기법

![화면 캡처 2021-11-24 015117](https://user-images.githubusercontent.com/88299729/143073115-dc292cbc-ed6f-43df-9c15-ad019355e123.png)

<br>

#### Knowledge distillation

* 학습된 큰 네트워크를 작은 네트워크의 학습 보조로 사용하는 방법
* Soft targets(soft outputs)에는 ground truth 보다 더 많은 정보를 담고 있음
  * e.g. 특정 상황에서 레이블 간의 유사도 등등

![화면 캡처 2021-11-24 015509](https://user-images.githubusercontent.com/88299729/143073158-00cc7e43-54c3-4528-87e7-b938e8fcce1f.png)

<br>

* Student network와 ground truth label의 cross-entropy
* Teacher network와 student network의 inference 결과에 대한 KLD loss로 구성

![화면 캡처 2021-11-24 015252](https://user-images.githubusercontent.com/88299729/143073176-2d159e11-a0f9-467b-9ad9-af510b0c8436.png)

**T**는 large teacher network의 출력을 smoothing(soften) 하는 역할을 한다.

**a** 는 두 loss의 균형을 조절하는 파라미터다.

<br>

#### Matrix / Tensor decomposition

* 하나의 Tensor를 작은 tensor들의 operation들의 조합(합, 곱)으로 표현하는 것
* Cp decomposition: rank 1 vector들의 outer product의 합으로 tensor를 approximation

![화면 캡처 2021-11-24 020702](https://user-images.githubusercontent.com/88299729/143073204-f088fc30-2f47-4d68-b039-cb58d6361b51.png)

<br>

#### Network Quantization

* 일반적으로 float32 데이터타입의 Network의 연산 과정을 그보다 작은 크기의 데이터 타입(e.g. float16, int8, etc)으로 변환하여 연산을 수행

![화면 캡처 2021-11-24 020942](https://user-images.githubusercontent.com/88299729/143073242-b534a60b-3588-4121-9259-4dc480a61207.png)

<br>

* 사이즈: 감소
* 성능(Acc): 일반적으로 약간 하락
* 속도: Hardware 지원 여부 및 사용 라이브러리에 따라 다름(향상 추세)
* Int8 quantization 예시(CPU inference, 속도는 pixel2 스마트폰에서 측정됨)

![화면 캡처 2021-11-24 021058](https://user-images.githubusercontent.com/88299729/143073270-6b881a33-613f-4e72-85fd-6f24479d9080.png)

<br>

#### Network Compiling

* 학습이 완료된 Network를 deploy하려는 target hardware에서 inference가 가능하도록 compile 하는 것(+ 최적화가 동반)
* 사실상 **속도에 가장 큰 영향**을 미치는 기법
* e.g. TensorRT(NVIDIA), Tflite(Tensorflow), TVM(apache), etc
* 각 compile library마다 성능 차이가 발생

![화면 캡처 2021-11-24 021418](https://user-images.githubusercontent.com/88299729/143073316-e072e035-8006-4eab-9b82-3d37051a68cc.png)

<br>

* compile 과정에서 layer fusion(graph optimization) 등의 최적화가 수행됨
* 예를 들어, tf의 경우 200개의 rule이 정의되어 있음

![화면 캡처 2021-11-24 021521](https://user-images.githubusercontent.com/88299729/143073329-527b02ab-d28f-4d84-8b01-40a018a574f2.png)

<br>

* Framework와 hardware backends 사이의 수많은 조합
* HW마다 지원되는 core, unit 수, instruction set, 가속 라이브러리 등이 다름

![화면 캡처 2021-11-24 021732](https://user-images.githubusercontent.com/88299729/143073382-d58152c9-7b78-4022-87fd-f6c5692c5474.png)

<br>

* 동일 회사의 hw임에도, Layer fusion의 조합에 따라 성능 차이가 발생 

![화면 캡처 2021-11-24 021830](https://user-images.githubusercontent.com/88299729/143073395-cdd45e7c-009f-4bd1-a1ca-aaeeb4046726.png)

<br>

* AutoML로 graph의 좋은 fushion을 찾아내자
* e.g. AutoTVM(Apache)

![화면 캡처 2021-11-24 021911](https://user-images.githubusercontent.com/88299729/143073409-61730d82-7cf6-4c43-9773-c4d1c13c4ee2.png)