# N-gram vs HMM 
전 주에서 공부한 HMM과 직접적인 비교를 통해 N-gram의 개념에 대한 이해를 해보고자 한다. 
일단, HMM의 최종적인 목표는(지난 주 과제를 기준으로) 

1. **특정 품사를 가진 단어 예측**:주어진 문장에서 각 단어에 가장 적합한 품사를 예측. 이 경우, 모델은 각 단어의 은닉 상태(품사)와 그 단어(관측된 상태) 사이의 관계를 학습하여, **다음에 올 단어의 품사를 예측** 한다. => 문장 내에서 단어의 순서와 품사 간의 확률적 관계를 이용하는 것이다.

2. **단어가 특정 품사를 갖는 것을 예측**: 이는 HMM을 통해 주어진 단어가 특정 품사를 가질 확률을 예측. HMM은 각 상태(품사) 전이의 확률과 각 상태에서 특정 단어(관측)가 나타날 확률을 모델링하는데, 이 정보를 통해 **문장 내의 각 단어에 대해 가장 가능성이 높은 품사를 태깅**할 수 있다.

> #### **HMM을 사용한 품사 태깅의 주 목적은 특정 단어 뒤에 어떤 단어가 올지 직접 예측하는 것이 아니다!**.
> 대신, HMM은 주어진 단어 시퀀스에서 각 단어의 품사를 예측하는 데 초점을 맞춘다. 즉, 문장 내 각 단어의 품사를 결정하는 것이 주된 목표인것.

#### 따라서, "특정 단어 뒤에 어떤 단어가 올지"를 예측하려면 다른 종류의 언어 모델(예: N-gram, 신경망 기반 모델 등)을 사용하는 것.

# N-gram
: N-gram은 주어진 시퀀스에서 **N개의 연속적인 항목**(보통은 단어)을 분석하는 모델. N-gram 모델에서는 (N-1)개의 단어가 주어졌을 때 N번째 단어의 등장 확률을 계산한다. 

> **N개의 연속적인 항목이란**, 텍스트 내에서 연속적으로 나타나는 N개의 단어(또는 문자)를 의미한다. 이 개념은 단순히 전체 문서에서 임의로 선택된 N개의 단어가 아니라, 실제로 텍스트 내에서 인접해 있는 N개의 단어 시퀀스를 가리킨다.

> 예를 들어, "The quick brown fox jumps over the lazy dog"이라는 문장이 있다고 할 때:
- 2-gram(바이그램)의 경우, 연속적인 항목의 예는 "the quick", "quick brown", "brown fox", "fox jumps". 각각은 문장 내에서 바로 옆에 있는 단어들로 구성된다. 
- 3-gram(트라이그램)에서는 "the quick brown", "quick brown fox", "brown fox jumps" 이런식으로..
  
> N-gram 모델에서는 이러한 N개의 연속적인 단어를 기반으로 하여 N+1번째 단어의 등장 확률을 예측하는것. 예를 들어, 바이그램 모델에서 "quick brown" 다음에 어떤 단어가 올 확률을 계산한다면, 이전에 나타난 "quick brown"이라는 바이그램에 기반하여 다음에 올 수 있는 단어의 확률 분포를 추정하는 것이다. 

#### 따라서 N-gram 모델에서 **N은 고려하는 문맥의 크기**를 나타내며, 이 문맥을 바탕으로 다음 단어를 예측. => **단어의 순서와 문맥이 모델에 반영**되어 더 정확한 언어 모델링이 가능해진다. 

# N-gram 모델 종류 
N-gram 모델은 문맥의 크기를 정의하는 N의 값에 따라 분류된다. 일반적인 N-gram 모델은 유니그램(Unigram), 바이그램(Bigram), 트라이그램(Trigram) 등이 있으며, N의 값이 커질수록 더 긴 문맥을 고려하게 된다. 

> N이 더 큰 N-gram 모델(예: 4-gram, 5-gram 등)은 더 긴 문맥을 고려할 수 있지만, 데이터의 희소성(sparsity) 문제가 심해지고, 계산 복잡도가 증가하는 문제가 있다. 따라서 실제 응용에서는 적절한 N의 크기를 선택하는 것이 중요하며, 이는 주로 사용할 데이터의 양과 작업의 특성에 따라 결정된다.
> **문맥이 길다고 큰 N-gram을 쓰는 것 은 아님.** 
더 긴 문맥을 사용하는 모델은 일반적으로 더 정확한 예측을 제공할 수 있지만, 모델의 복잡성, 처리 시간, 필요한 데이터의 양도 함께 증가한다는 점을 고려해야 함.


- **유니그램 (Unigram)**:
- 
![image](https://github.com/JinnyKo/NLP-Specialization-Coursera/assets/93627969/a8618beb-8228-4721-a22d-e5992260b7d5)

유니그램 모델은 N이 1인 경우로, 각 단어의 등장 확률을 독립적으로 계산한다. 즉, 문맥을 전혀 고려하지 않고 각 단어가 개별적으로 나타날 확률만을 사용환다.
유니그램 모델의 단점은 문맥이나 단어의 순서를 전혀 고려하지 않는다는 것.

- **바이그램 (Bigram)**:
- 
![image](https://github.com/JinnyKo/NLP-Specialization-Coursera/assets/93627969/eb24a21b-ec42-4973-b0c5-bc5a6e851686)

바이그램 모델은 N이 2인 경우로, 바로 앞에 오는 하나의 단어를 문맥으로 고려하여 다음 단어의 확률을 계산한다. 바이그램 모델은 인접한 단어 간의 관계를 반영할 수 있다.
바이그램 모델은 유니그램보다는 문맥을 더 고려하지만, 여전히 제한적인 문맥 정보만을 사용.

- **트라이그램 (Trigram)**:

![image](https://github.com/JinnyKo/NLP-Specialization-Coursera/assets/93627969/4690045c-3926-44a5-8ec1-8e0ec056cc36)

트라이그램 모델은 N이 3인 경우로, 이전의 두 단어를 문맥으로 고려하여 다음 단어의 확률을 계산한다. 트라이그램은 바이그램보다 더 넓은 범위의 문맥을 고려할 수 있다.
더 넓은 문맥을 고려하므로 바이그램보다 일반적으로 더 정확한 예측을 하지만 모델의 복잡도와 요구되는 데이터 양이 증가하는 단점이 있다. 


