# 16_통계적 언어 모델(Statistical Language Model, SLM)

앞 문서에서 언어 모델(Language Model)의 개념에 대해서 간략히 설명했다. 여기서는 언어 모델의 전통적인 접근 방법인 통계적 언어 모델을 소개한다. 통계적 언어 모델이 통계적인 접근 방법으로 어떻게 언어를 모델링하는지 배워본다. 통계적 언어 모델(Statistical Language Model)은 줄여서 SLM이라고 한다. 



## 1. 조건부 확률

조건부 확률은 두 확률 P(A), P(B)에 대해서 아래와 같은 관계를 갖는다. 

$$
p(B|A) = P(A,B)/P(A)
$$

$$
P(A,B) = P(A)P(B|A)
$$

더 많은 확률에 대해 일반화해보자. 4개의 확률이 조건부 확률의 관계를 가질 떄, 아래와 같이 표현할 수 있다. 
$$
P(A,B,C,D)=P(A)P(B|A)P(C|A,B)P(D|A,B,C)
$$
이를 조건부 확률의 연쇄법칙(chain rule)이라고 한다. 이제는 4개가 아닌 n개에 대해서 일반화를 진행해보자. 
$$
P(x_{1}, x_{2}, x_{3}...x_{n})=P(x_{1})P(x_{2}|x_{1})P(x_{3}|x_{1},x_{2})..P(x_{n}|x_{1}...x_{n-1})
$$
조건부 확률에 대한 정의를 통해 문장의 확률을 구해보자. 



## 2. 문장에 대한 확률

문장 'An adorable little boy is spreading smiles'의 확률
$$
P(An\ adorable \ little \ boy \ is \ spreading \ smiles)
$$
를 식으로 표현해보자. 

각 단어는 문맥이라는 관계로 인해 이전 단어의 영향을 받아 나온 단어이다. 그리고 모든 단어로부터 하나의 문장이 완성된다. 그렇기 떄문에 문장의 확률을 구하고자 조건부 확률을 사용한다. 앞서 언급한 조건부 확률의 일반화 식을 문장의 확률 관점에서 다시 적어보면, 문장의 확률은 각 단어들이 이전 단어가 주어졌을 때 다음 단어로 등장할 확률의 곱으로 구성된다. 
$$
P(w_{1},w_{2}, w_{3}, w_{4}, w_{5},...w_{n}) = \prod_{n=1}^n P(w_{n}|w_{1},...,w_{n-1})
$$
위의 문장에 해당 식을 적용해보면 다음과 같다. 
$$
P(An\ adorable\ little\ boy\ is \ spreading \ smiles) = \\
P(An)\times P(adorable|An)\times P(boy|An\ adorable)\times P(is|An\ adorable\ little\ boy)\times P(spreading|An\ adorable\ little\ boy\ is)\times P(smiles|An\ adorable\ little\ boy\ is\ spreading)
$$
문장의 확률을 구하기 위해서 각 단어에 대한 예측 확률들을 곱한다. 



## 3. 카운트 기반의 접근

문장의 확률을 구하기 위해서 다음 단어에 대한 예측 확률을 모두 곱한다는 것은 알았다. 그렇다면 SLM은 이전 단어로부터 다음 단어에 대한 확률을 어떻게 구할까? 정답은 카운트에 기반하여 확률을 계산하는 것이다. <br>



An adorable little boy가 나왔을 때, is가 나올 확률인 
$$
P(is|An\ adorable\ little\ boy)
$$
를 구해보자. 
$$
P(is|An\ adorable\ little\ boy)= {count(An\ adorable\ little\ boy\ is) \over count(An\ adorable\ little\ boy)}
$$
그 확률은 위와 같다. 예를 들어 기계가 학습한 코퍼스 데이터에서 An adorable little boy가 100번 등장했는데 그 다음에 is가 등장한 경우는 30번이라고 하자. 이 경우 P(is|An adorable little boy)는 30%가 된다. 



## 4. 카운트 기반 접근의 한계 - 희소 문제(Sparsity Problem)

언어 모델은 실생활에서 사용되는 언어의 확률 분포를 근사 모델링한다. 실제로 정확하게 알아볼 방법은 없겠지만 현실에서도 An adorable little boy가 나왔을 때 is가 나올 확률이 존재한다. 이를 실제 자연어의 확률 분포, 현실에서의 확률 분포라고 명칭한다. 기계에게 많은 코퍼스를 훈련시켜서 언어 모델을 통해 현실에서의 확률 분포를 최대한 근사하는 것이 언어 모델의 목표라고 할 수 있다. 그런데, 카운트 기반으로 접근하려 한다면 갖고 있는 코퍼스(corpus) 즉, 기계가 훈련하는 데 필요한 데이터의 양이 지나치게 방대하다는 문제가 발생한다. 

