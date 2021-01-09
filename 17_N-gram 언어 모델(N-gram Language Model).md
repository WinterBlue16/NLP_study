# 17_N-gram 언어 모델(N-gram Language Model)

n-gram 언어 모델은 여전히 카운트에 기반한 통계적 접근을 사용하고 있으므로 통계적 언어 모델의 일종이라 할 수 있다. 그러나, 앞서 배운 모델과는 달리 이전에 등장한 모든 단어를 고려하는 것이 아니라 일부 단어만 고려하는 접근 방법을 사용한다. 그리고 이 때 일부 단어를 몇 개 보느냐를 결정하는데, n-gram에서의 n은 바로 이것을 의미한다. 



## 1. 코퍼스에서 카운트하지 못하는 경우의 감소

 SLM(통계적 언어 모델)의 한계는 훈련 코퍼스에 확률을 계산하고 싶은 문장이나 단어가 없을 수 있다는 점이다. 또한 확률을 계산하고 싶은 문장이 길어질수록 갖고 있는 코퍼스에서 그 문장이 존재하지 않을 가능성이 높다. 다시 말해 카운트할 수 없을 가능성이 높다는 것이다. 하지만 다음과 같이 참고하는 단어들을 줄이면 카운트를 할 수 있는 가능성을 높일 수 있다. 
$$
P(is|An\ adorable \ little \ body)\approx \ P(is|boy)
$$

가령, An adorable little boy가 나왔을 때 is가 나올 확률을 그냥 boy가 나왔을 때 is가 나올 확률로 생각하보자. 갖고 있는 코퍼스에 An adorable little boy is가 있을 가능성보다는 boy is라는 더 짧은 단어 시퀀스가 존재할 가능성이 더 높다. 조금 지나친 일반화로 느껴진다면 아래와 같이 little boy가 나왔을 때 is가 나올 확률로 생각하는 것도 대안이다. 
$$
P(is|An\ adorable \ little \ body)\approx \ P(is|little\ boy)
$$
즉, 앞에서는 An adorable little boy가 나왔을 때 is가 나올 확률을 구하기 위해서는 An adorable little boy가 나온 횟수와 An adorable little boy is가 나온 횟수를 카운트 해야만 했다. 하지만 이제는 단어의 확률을 구하고자 기준 단어의 앞 단어를 전부 포함해서 카운트하는 게 아니라, 앞 단어 중 임의의 개수만 포함해서 카운트해 근사하자는 것이다. 이렇게 하면 갖고 있는 코퍼스에서 해당 단어의 시퀀스를 카운트할 확률이 높아진다. 



## 2. N-gram 

이 때 임의의 개수를 정하기 위한 기준을 위해 사용하는 것이 n-gram이다. n-gram은 n개의 연속적인 단어 나열을 의미한다. 갖고 있는 코퍼스에서 n개의 단어 뭉치 단위로 끊어서 이를 하나의 토큰으로 간주한다. 예를 들어 문장 An adorable little boy is spreading smiles이 있을 때, 각 n에 대해서 n-gram을 전부 구해보면 다음과 같다. 



**uni**grams : an, adorable, little, boy, is, spreading, smiles

**bi**grams : an adorable, adorable little, little boy, boy is, is spreading, spreading smiles

**tri**grams : an adorable little, adorable little boy, little boy is, boy is spreading, is spreading smiles

**4**-gram : an adorable little boy, adorable little boy is, little boy is spreading, boy is spreading smiles



n-gram을 사용할 때는 n이 1일 때는 유니그램(unigram), 2일 때는 바이그램(bigram), 3일 때는 트라이그램(trigram)이라고 명명하며, n이 4 이상일 때는 gram 앞에 그대로 숫자를 붙여서 명명한다. 출처에 따라서는 유니그램, 바이그램, 트라이그램 또한 각각 1-gram, 2-gram, 3-gram이라고 하기도 한다. 이제 n-gram을 이요한 언어 모델을 설계해보도록 하자. 



n-gram을 통한 언어 모델에서는 다음에 나올 단어의 예측은 오직 n-1개의 단어에만 의존한다. 예를 들어 **'An adorable little boy is spreading'** 다음에 나올 단어를 예측하고 싶다고 할 때, n=4라고 한 4-gram을 이용한 언어 모델을 사용한다고 하자. 이 경우, spreading 다음에 올 단어를 예측하는 것은 n-1에 해당하는 앞의 3개의 단어인 것이다. 

![img](https://wikidocs.net/images/page/21692/n-gram.PNG)