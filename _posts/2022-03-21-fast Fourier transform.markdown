---
layout: post
title: "고속 푸리에 변환(Fast Fourier transform)"
subtitle: "FFT"
date: 2020-01-31 14:45:13 -0400
background: '/img/posts/06.jpg'
---
# __고속 푸리에 변환(fast Fourier transform)__
고속 푸리에 변환(Fast Fourier transform)은 이산 푸리에 변환과 그 역변환을 빠르게 수행하는 효율적인 알고리즘이다. FFT는 디지털 신호 처리에서 편미분 방정식의 근을 구하는 알고리즘에 이르기까지 많은 분야에서 사용한다.

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/aaa6796c91e957587336d38b39c994879f8e04bb)이 복소수라고 가정할 때, DFT는 다음과 같이 정의한다.

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/215ef69b19baa34155ef751206bf77d826515677)
이 식을 정의에 따라 계산하면 O(n2)의 연산이 필요하지만, FFT를 이용하면 O(n log n)의 연산만으로 가능하다. n이 합성수일 경우 그 소인수 분해를 이용하여 연산 횟수를 줄일 수는 있지만, FFT를 사용하면 n이 소수일 경우에도 O(n log n)번의 연산 횟수를 보장한다.

## __쿨리-튜키 알고리즘__
가장 일반적으로 사용되는 FFT 알고리즘은 쿨리-튜키 알고리즘(Cooley-Tukey algorithm)이다. 이 알고리즘은 분할 정복 알고리즘을 사용하며, 재귀적으로 n 크기의 DFT를 n = n1 n2가 성립하는 n1, n2 크기의 두 DFT로 나눈 뒤 그 결과를 O(n) 시간에 합치는 것이다. 이 방법은 1965년에 J. W. 쿨리와 J. W. 튜키가 발표하여 널리 알려졌지만, 나중에 카를 프리드리히 가우스가 1805년에 같은 방법을 이미 개발하였으며, 그 뒤에도 제한된 형태의 FFT가 종종 발견되었음이 밝혀졌다.

쿨리-튜키 알고리즘은 보통 크기 n을 재귀적으로 2등분하여 분할 정복을 적용하기 때문에 n = 2k인 경우에 많이 적용된다. 하지만 일반적으로 n1과 n2는 같을 필요가 없으며, 따라서 n이 임의의 합성수일 때에도 적용 가능하다. 쿨리-튜키 알고리즘은 DFT를 더 작은 크기의 DFT로 나누기 때문에, 뒤에 설명된 다른 FFT 알고리즘과 함께 사용될 수 있다.