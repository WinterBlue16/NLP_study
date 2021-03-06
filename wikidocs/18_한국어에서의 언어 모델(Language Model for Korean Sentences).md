# 18_한국어에서의 언어 모델(Language Model for Korean Sentences)

영어나 기타 언어에 비해 한국어는 언어 모델로 다음 단어를 예측하기가 훨씬 까다로운 편이다. 그 이유는 다음과 같다. 

## 1) 한국어는 어순이 중요하지 않다.

한국어는 영어나 기타 언어에 비해 어순이 중요하지 않다. 이 말의 뜻은 정말로 어순이 중요하지 않다는 뜻이 아니라, 어순이 규칙에 따라 배열되지 않더라도 문장 전체의 의미를 이해하는 데 큰 지장이 없다는 것이다. 이러한 예시는 아래와 같다. <br>



Ex) 

① 나는 운동을 합니다 체육관에서.
② 나는 체육관에서 운동을 합니다.
③ 체육관에서 운동을 합니다.
④ 나는 운동을 체육관에서 합니다.

<br>

위의 문장들은 전부 의미가 통한다. 심지어 '나는'이라는 주어를 생략해도 의미가 통하는 것을 확인할 수 있다. 이렇게 단어 순서를 뒤죽박죽으로 바꾸어놔도 한국어는 의미가 전달되기 때문에 확률에 기반한 언어 모델로 다음 단어를 예측하기가 쉽지 않다. 

## 2) 한국어는 교착어이다.

한국어는 교착어이다. '교착어'란 실질적인 의미를 가진 단어 또는 어간에 문법적인 기능을 가진 요소가 차례로 결합함으로써 문장 속에서의 문법적인 역할이나 관계의 차이가 나타나는 언어이다. 이러한 언어는 한국어 외에도 일본어, 터키어, 핀란드어 등이 있다. <br>

이러한 언어들의 특징은 언어 모델 작동을 어렵게 만든다. 띄어쓰기 단위인 어절 단위로 토큰화를 할 경우 문장에서 발생 가능한 단어의 수가 기하급수적으로 늘어난다. 대표적인 예로 한국어에는 '조사'가 있다. 영어는 기본적으로 조사가 존재하지 않는다. 하지만 한국어의 경우 어떤 행동을 가리키는 동사의 주어나 목적어를 위한 조사가 존재한다. <br>

가령 '그녀'라는 단어 하나만 해도 그녀가, 그녀를, 그녀의, 그녀와, 그녀로, 그녀에게, 그녀처럼 등과 같이 다양한 경우가 파생된다. 그렇기 때문에 한국어에서는 **토큰화**를 통해 접사나 조사 등을 분리하는 것은 중요한 작업이 될 수밖에 없다. 

## 3) 한국어는 띄어쓰기가 제대로 지켜지지 않는다.

한국어는 띄어쓰기를 제대로 하지 않아도 의미가 전달되며, 띄어쓰기 규칙 또한 상대적으로 까다로운 언어이다. 그 때문에 자연어 처리를 하는 것에 있어서 한국어 코퍼스는 띄어쓰기가 제대로 지켜지지 않는 경우가 많다. 그러나 토큰이 제대로 분리되지 않은 채 훈련 데이터로 사용된다면 언어 모델은 제대로 작동하지 않으므로 주의해야 한다.

