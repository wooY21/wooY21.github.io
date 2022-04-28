# Ford-Fulkerson Algorithm
Ford-Fulkerson Algorithm은 residual network를 활용해 Max Flow를 구하는 기법이다. 그렇다면 Max Flow Algorithm이란 무엇일까?  

## Max Flow Algorithm
Max Flow Algorithm이란 가중치가 있는 directed graph [G]와 source node [s], sink node [t]가 주어졌을 때 각 edge의 용량을 고려하여 s에서 t로 흘려보낼 수 있는 Max Flow를 구하는 알고리즘을 가리킨다. 전력, 수도, 통신 등 다양한 분야에서 활용되고 있다.  

G의 각 엣지 가중치를 capacity라고 하며 (u,v)의 capacity는 c(u,v)라고 쓴다. 이때 capacity >= 0 이다. 노드 u와 v 사이를 흐르는 net flow는 f(u,v)라고 쓰며 유량은 real-value function이다. Max Flow Algorithm 에는 세가지 제약이 존재한다.  
__capacity constraint : f(u,v)≤c(u,v), 유량이 용량보다 클 수는 없다.
skew symmetry : f(u,v)=−f(v,u)
flow conservation : 각 node에서 유량은 새로 더해지거나 감소하지 않는다.__  

