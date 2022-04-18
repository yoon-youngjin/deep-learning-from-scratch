## 2장 퍼셉트론
> 신경망(딥러닝)의 기원이 되는 알고리즘
> 
> 다수의 신호를 받아, 하나의 신호를 출력해주는 구조
> 
> 출력값은 0 또는 1

![image](https://user-images.githubusercontent.com/83503188/162928622-229230c7-5453-444c-a39a-5ce432b5752d.png)

> x1, x2를 입력 신호
> 
> y는 출력 신호
> 
> w1, w2는 가중치 

- 그림의 원을 **뉴런** 혹은 **노드** 
- 입력 신호가 뉴런에 보내질 때는 각각 고유한 **가중치** 가 곱해짐
  - 가중치가 클수록 해당 신호가 더 중요함을 의미 


### AND GATE

![image](https://user-images.githubusercontent.com/83503188/160584122-d9073bff-e3e1-404f-ad23-80505c27acf7.png)


### NAND GATE
![image](https://user-images.githubusercontent.com/83503188/160584210-2d682752-536a-4fe9-8a8d-ef1f0bc13599.png)

### OR GATE

![image](https://user-images.githubusercontent.com/83503188/160584286-129621c1-2013-424c-93dd-2b6d20c18f65.png)

- `편항`값이 작아진 모습

### XOR GATE

![image](https://user-images.githubusercontent.com/83503188/160584415-dcc18647-ede1-4d11-942f-749ecd3889da.png)

- 단층 퍼셉트론으로 표현할 수 없음

> 학습?
> 
> 적절한 매개변수 값을 정하는 작업 

### 정리
> **이번 장에서 배운 내용**
* 퍼셉트론은 입출력을 갖춘 알고리즘이다. 입력을 주면 정해진 규칙에 따른 값을 출력한다.
* 퍼셉트론에서는 ‘가중치’와 ‘편향’을 매개변수로 설정한다.
* 퍼셉트론으로 AND, OR 게이트 등의 논리 회로를 표현할 수 있다.
* XOR 게이트는 단층 퍼셉트론으로는 표현할 수 없다.
* 2층 퍼셉트론을 이용하면 XOR 게이트를 표현할 수 있다.
* 단층 퍼셉트론은 직선형 영역만 표현할 수 있고, 다층 퍼셉트론은 비선형 영역도 표현할 수 있다.
* 다층 퍼셉트론은 (이론상) 컴퓨터를 표현할 수 있다.


