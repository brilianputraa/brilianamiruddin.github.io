---
layout: post
title: "[MLOps] Machine Learning Powered Applications - ML Project Success Measurement (머신러닝 프로젝트의 성공 측정하기)"
categories: study-log
tags: [machine learning, mlops]
author:
  - Brilian Putra Amiruddin
---

<img src="https://images.unsplash.com/photo-1583833008338-31a6657917ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80" alt="drawing" style='height: 70%; width: 70%; object-fit: contain'/>

As we know, in order to develop good machine learning models, the first step we need to consider is the product’s request matter and we suppose to make the first model the most simple model to address what the product’s need (제품의 요구 사항에 맞는 가장 간단한 모델이어야 한다). Because we can swiftly make iteration progress on ML as soon as there are results. 

Referring to the book, there are 3 steps covered to increase our model complexity for [ML Editor](#linknote)
 (머신러닝 에디터의 복잡도를 높일 가능성이 있는 세 가지 방법을 다루었다).



1. Baseline Model: Designing Heuristics Based on Domain Knowledge (기준 모델: 도메인 지식을 활용해 경험적인 규칙을 설계한다)

    Start simply by defining the rules based on prior knowledge of what makes content is well-written. Then we can test the rules by looking if the rules help differentiate between well-written text or poorly written text.


    좋은 글을 작성하는 방법에 대한 지식을 활용해 스스로 규칙을 정의한다. 이런 규칙이 잘 쓰인 글과 그렇지 못한 글을 구분하는 데 도움이 되는지 테스트이다.

2. Simple Model: Classifying Text as Good or Bad, and Using the Classifier to Generate Recommendations (단순한 모델: 텍스트가 좋은지 아닌지 분류하고 분류기를 사용해 추천을 생성한다)

    We could train a simple model to differentiate the good or bad written questions. Provided that the model performs well, we can then inspect and use it to get the features that be highly predictive of a good question and use those features as recommendations. 


    좋은 질문과 나쁜 질문을 구분하는 간단한 모델을 훈련한다. 모델이 잘 동작하면 좋은 질문을 예측하는 데 뚜어난 특성을 조사하고 이 특성을 사용해 추천을 만든다.

3. Complex Model: Training an End-to-End Model that Goes From Bad Text to Good Text (보잡한 모델: 나쁜 텍스트를 좋은 텍스트로 바꾸는 엔드투엔드 모델을 훈련한다)

    In terms of model and data, this part is the most complex approach. However, if we had the resources to gather the training data and build also maintain a complex model, we could solve the product requirements directly.


    모델과 데이터 측면에서 사장 복잡한 방법이다. 그런데, 훈련 데이터 수집과 복잡한 모델을 유지할 수 있는 자원을 보유하고 있다면 제품의 요구 사항을 바로 해결할 수 있다.


Depending on the cases, all of these three approaches are different and might be evolving as we learn more from the prototypes along the way. But when working on ML, you should define a common set of metrics to compare the success of modeling pipelines (머신러닝으로 진행할 때는 모델 파이프라인의 성능을 비교하기 위해서 공통된 측정 지표를 정의해야 된다).

###### <a name="linknote"></a> **ML Editor** is a project by the book author, which creates an ML-based question editor on a forum such as the stack exchange.

