## Beam Search & BLEU Score



### Greedy decoding

기존에 단어를 예측 할 때, 앞에서부터 현재 time step에서 가장 좋아보이는 단어를 그때그때 선택하는 decoding 방법이다.



> Greedy decoding의 문제점!

​	한번 잘못 예측을 하면 다시 돌아가서 고칠 수가 없고, 계속 잘못된 예측을 할 수 밖에 없다.



#### 어떻게 해결 할 수 있을까?



* **Exhaustive search**

  

  ![화면 캡처 2021-09-10 134811](https://user-images.githubusercontent.com/88299729/132803072-f58e4696-645e-4404-846a-fa95d1174f35.png)

  

   **모든 가능한 sequence들에 대해서 가장 높은 joint probability를 구한다**. 이 과정 속에서, 그때그때 가장 높은 확률 값을 선택하는 것이 아닌, 총 확률 값이 가장 높은 것을 선택하기 위해 지금은 낮은 확률을 선택 할 수도 있다.

  > 단점

  ​	V<sup>t</sup>번의 너무 많은 경우를 고려해야 한다.



* **Beam Search**

  

  ![화면 캡처 2021-09-10 124354](https://user-images.githubusercontent.com/88299729/132803046-c148e535-f885-452c-aaa8-92a80cf1175a.png)

  * Exhaustive search에서 너무 많은 경우를 고려해야 되는 부분을 개선해서 나온 방법이다. 매 타임 스텝마다 **정해놓은 K개의 가능한 가짓 수를 고려**하고, 마지막까지 decoding을 진행한 후 K개의 **candidate 중에서 가장 확률이 높은 것**을 택한다.
    * K는 beam size를 의미하고 대체로 5~10정도로 설정한다.
  * ![화면 캡처 2021-09-10 135536](https://user-images.githubusercontent.com/88299729/132803239-beb5cb73-cddc-462e-ae0d-f5679b54c8a7.png)
  * 최대화 하고자 하는 값은 P<sub>LM</sub> 이고 joint probability를 의미한다.
  * log를 취해줌으로서 곱하기 연산이 더하기 연산으로 바뀌게 되고, 마이너스 값을 계속 더해주게 된다.



​		서로 다른 경로(hypotheses)가 존재하고 서로 다른 시점에 <END> 토큰을 생성 할 수 있다.

​		문제점 : 비교적 짧은 hypotheses는 높은 확률을 가지고, 긴 hypotheses는 낮은 확률을 가진다. (길이가 길어						짐에 따라 - 값을 더해주는 연산이 많아지기 때문이다.)

​		해결법 : 각 hypotheses를 만들어진 단어의 개수로 나누어준다.



![화면 캡처 2021-09-10 140357](https://user-images.githubusercontent.com/88299729/132803347-af6fd23c-c4a4-4cbe-9bd3-751ba6bc3d70.png)



### Precision and Recall

언어의 평가는 단순히 같은 단어가 같은 위치에 나온 것으로 평가 할 수 없다.

ex)

![화면 캡처 2021-09-10 130213](https://user-images.githubusercontent.com/88299729/132803098-a7892183-5645-4112-8447-27bf877df044.png)

#### 산술, 기하, 조화 평균

![화면 캡처 2021-09-10 131201](https://user-images.githubusercontent.com/88299729/132803116-ac199af1-d2d3-4f06-b061-f74df09bf6a1.png)

![화면 캡처 2021-09-10 133050](https://user-images.githubusercontent.com/88299729/132803184-e34d0000-813f-4412-813d-b81013fda033.png)

#### F-measure (조화 평균)

![image](https://user-images.githubusercontent.com/88299729/132803433-26d57575-ba38-4fcb-8ec2-6f8525cdb15a.png)

![화면 캡처 2021-09-10 140525](https://user-images.githubusercontent.com/88299729/132803377-51aded38-8e57-4730-afbb-aa5db5db4c09.png)



> 문제점

​	각각의 word의 위치는 다르더라도 같은 문자가 나오면 문법적으로 완전 틀린 문장일지라도 확률이 100프로가 	나온다.



![화면 캡처 2021-09-10 140856](https://user-images.githubusercontent.com/88299729/132803443-c06b4d95-26ee-46da-b1c3-13a89e92924e.png)



### BLEU Score

![화면 캡처 2021-09-10 140913](https://user-images.githubusercontent.com/88299729/132803470-f85e6175-9a8f-46d2-a6dd-70dbcb0f0d90.png)



* N-gram으로 precision 값을 계산하여 기하 평균을 이용한다.
  * N-gram은 연속된 N개의 원소를 가진 부분 sequence이다.
* recall 의 최대 값을 min(1, length of prediction / length of reference) 로 알 수 있다. 이를, brevity penalty 라고 부른다.



> 함께 구해보자!

![화면 캡처 2021-09-10 133752](https://user-images.githubusercontent.com/88299729/132803196-08853f37-6c0a-4e3b-af1d-001e54f0ba66.png)



