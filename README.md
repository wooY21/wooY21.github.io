# Ford-Fulkerson Algorithm
Ford-Fulkerson Algorithm은 residual network를 활용해 Max Flow value를 구하는 기법이다. 그렇다면 Max Flow value란 무엇일까?  

## Max Flow Algorithm
Max Flow Algorithm이란 가중치가 있는 directed graph [G]와 source node [s], sink node [t]가 주어졌을 때 각 엣지의 용량(capacity)을 고려하여 s에서 t로 흘려보낼 수 있는 최대 유량(flow)을 구하는 알고리즘을 가리킵니다. 전력, 수도, 통신 등 다양한 분야에서 폭넓게 쓰이고 있습니다. 용어 및 개념 몇 가지 살펴보겠습니다.

G의 각 엣지 가중치를 용량(capacity)라고 하며 (u,v)의 용량을 c(u,v)라고 씁니다. 용량은 항상 0 이상입니다. 노드 u와 v 사이를 흐르는 유량(net flow)은 f(u,v)라고 쓰며 유량은 실수치 함수(real-valued function)입니다. 최대 유량 문제에는 다음 세 가지 제약조건이 있습니다. 곱씹어보면 상식적인 것들입니다.
