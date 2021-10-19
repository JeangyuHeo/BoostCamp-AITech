## Passage Retrieval – Scaling Up

### Passage Retrieval and Similarity Search

####  복습 - Retrieval with dense embedding

* **동작 구조** 

![화면 캡처 2021-10-19 142400](https://user-images.githubusercontent.com/88299729/137854109-c9383314-df81-4359-b5be-a0670b0e7742.png)

* **inference**
  * Passage와 query를 각각 임베딩한 후 query로부터 거리가 가까운 순서대로 passage에 순위를 매김

![화면 캡처 2021-10-19 142728](https://user-images.githubusercontent.com/88299729/137854317-e1922c9f-cb1b-413c-ae2c-7ae9bb6f8a37.png)

#### MIPS(Maximum Inner Product Search)

* 주어진 질문(query) vector q에 대해 Passage vector v들 중 가장 질문과 관련된 벡터를 찾아야 함
  * 여기서 관련성은 내적(inner product)이 가장 큰 것

![화면 캡처 2021-10-19 143003](https://user-images.githubusercontent.com/88299729/137854783-1186bc0e-18b7-48a8-855b-5788e2933019.png)

* 4, 5 강에서 사용한 검색 방법: brute-force(exhaustive) search
  * 저장해둔 모든 Sparse/Dense 임베딩에 대해 일일히 내적 값을 계산하여 가장 값이 큰 passage를 추출



#### MIPS in Passage Retrieval

![화면 캡처 2021-10-19 143324](https://user-images.githubusercontent.com/88299729/137854804-04e1bed6-ff3e-43a5-8cf9-11b7d96bfdee.png)

#### MIPS & Challenges

* 실제로 검색해야 할 데이터는 훨씬 방대함
  * 5백만개(위키피디아)
  * 수십 억, 조 단위까지 커질 수 있음
  * => 따라서, 더이상 모든 문서 임베딩을 일일히 보면서 검색 할 수 없음



#### Tradeoffs of similarity search

![화면 캡처 2021-10-19 143858](https://user-images.githubusercontent.com/88299729/137854849-a75c1f69-abff-40d4-beda-999c778dd952.png)

##### 1) Search Speed

* 쿼리당 유사한 vector를 k개 찾는데 얼마나 걸리는지?
  * => 가지고 있는 벡터량이 클수록 더 오래 걸림

##### 2) Memory Usage

* 벡터를 사용할 때, 어디에서 가져올 것인지?
  * => RAM에 모두 올려둘 수 있으면 빠르지만, 많은 RAM 용량을 요구함
  * => 디스크에서 계속 불러와야한다면 속도가 느려짐

##### 3) Accuracy

* brute-force 검색 결과와 얼마나 비슷한지?
  * => 속도를 증가시키려면 정확도를 희생해야 하는 경우가 많음



![화면 캡처 2021-10-19 143931](https://user-images.githubusercontent.com/88299729/137854909-a97f1e53-fa3b-427e-bc3d-236407dd3917.png)



#### Increasing search space by bigger corpus

* corpus 의 크기가 커질수록

  * 탐색 공간이 커지고, 검색이 어려워짐
  * 저장해 둘 memory space 또한 많이 요구됨
  * Spare Embedding의 경우 이러한 문제가 훨씬 심함

  e.g. 1M docs, 500K distinct terms = 2TB

  ![화면 캡처 2021-10-19 144140](https://user-images.githubusercontent.com/88299729/137854926-88d0908d-134f-4a25-bbc5-ed44bcaca08a.png)

### Approximating Similarity Search

#### Compression -Scalar Quantization (SQ)

![화면 캡처 2021-10-19 144743](https://user-images.githubusercontent.com/88299729/137854952-d4f0e682-0a56-46bf-b452-e721311e1cff.png)

Compression: vector를 압축하여, 하나의 vector가 적은 용량을 차지 => 압축량 ↑ => 메모리 ↓, 정보 손실 ↑

e.g. Scalar quantization: 4-byte floating point =>1-byte (8bit) unsigned integer로 압축



#### Pruning - Inverted File (IVF)

![화면 캡처 2021-10-19 145252](https://user-images.githubusercontent.com/88299729/137854990-3483a657-af40-4982-b696-45ff4e3e63f4.png)

Pruning: Search space를 줄여 search 속도 개선 (dataset의 subset만 방문)

=> Clustering + Inverted file을 확용한 search

1) **Clustering**: 전체 vector space를 k 개의 cluster로 나눔 (e.g. k-means clustering)

2. **Inverted file (IVF)**
   * Vector의 index = inverted list structure
   * => (각 cluster의 centroid id)와 (해당 cluster의 vector들)이 연결되어있는 형태

- **Searching with clustering and IVF**

i) 주어진 query vector에 대해 근접한 centroid vector를 찾음

ii) 찾은 cluster의 inverted list 내 vector들에 대해 search 수행



### Introduction to FAISS

![화면 캡처 2021-10-19 150505](https://user-images.githubusercontent.com/88299729/137855018-724a8c2b-5db6-4db4-9256-f830fa320fcd.png)

#### What is FAISS

FAISS : Library for efficient similarity search

![화면 캡처 2021-10-19 150821](https://user-images.githubusercontent.com/88299729/137855043-c4d61405-6bc2-47d4-8489-96cf64d42be4.png)

#### Passage Retrival with FAISS

1) **Train index and map vectors**

   ![화면 캡처 2021-10-19 150925](https://user-images.githubusercontent.com/88299729/137855079-ee2272ab-a93c-4d74-beb5-f57995848e50.png)

2) **Search based on FAISS index**

   * *nprobe: 몇 개의 가장 가까운 cluster를 방문하여 search 할 것인지

     ![화면 캡처 2021-10-19 151036](https://user-images.githubusercontent.com/88299729/137855113-a43d5f52-be5b-4c61-8bf4-0aea033b44ee.png)



### Scaling up with FAISS

#### FAISS Basics

![화면 캡처 2021-10-19 151245](https://user-images.githubusercontent.com/88299729/137855139-76d55227-a3ff-4cb6-aa3c-2d618fe9cb4a.png)



#### IVF with FAISS

![화면 캡처 2021-10-19 151309](https://user-images.githubusercontent.com/88299729/137855233-a0dbcdaa-6cf4-407b-9bc4-ae1e4f39f2b8.png)

#### IVF-PQ with FAISS

![화면 캡처 2021-10-19 151336](https://user-images.githubusercontent.com/88299729/137855264-0cbd0f38-b159-44bc-8a8c-7ae2d3eb20e9.png)

#### Using GPU with FAISS

![화면 캡처 2021-10-19 151434](https://user-images.githubusercontent.com/88299729/137855345-b69207b2-5035-43ff-a043-4e6bc72164cf.png)

#### Using Multiple GPUs with FAISS

![화면 캡처 2021-10-19 151544](https://user-images.githubusercontent.com/88299729/137855421-e3864f1b-4231-4932-ba8b-8d32dae519f6.png)