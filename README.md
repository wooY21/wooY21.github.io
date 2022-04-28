# Ford-Fulkerson Algorithm
Ford-Fulkerson Algorithm은 residual network를 활용해 Max Flow를 구하는 기법이다. 그렇다면 Max Flow Algorithm이란 무엇일까?  

## Max Flow Algorithm
Max Flow Algorithm이란 가중치가 있는 directed graph [G]와 source node [s], sink node [t]가 주어졌을 때 각 edge의 용량을 고려하여 s에서 t로 흘려보낼 수 있는 Max Flow를 구하는 알고리즘을 가리킨다. 전력, 수도, 통신 등 다양한 분야에서 활용되고 있다.  

G의 각 엣지 가중치를 capacity라고 하며 (u,v)의 capacity는 c(u,v)라고 쓴다. 이때 capacity >= 0 이다. 노드 u와 v 사이를 흐르는 net flow는 f(u,v)라고 쓰며 유량은 real-value function이다. Max Flow Algorithm 에는 세가지 제약이 존재한다.  
__capacity constraint : f(u,v)≤c(u,v), 유량이 용량보다 클 수는 없다.
skew symmetry : f(u,v)=−f(v,u)
flow conservation : 각 node에서 유량은 새로 더해지거나 감소하지 않는다.__  

다음은 표기 방법이다. 만약 용량 정보가 c(u,v) = 10,  c(v,u)=6 라면 다음과 같이 표시할 수 있다.
![image](https://user-images.githubusercontent.com/101376961/165784395-5742b281-9590-4414-9fc5-3e5c2811a570.png)  
여기에서 만약 u > v 의 유량이 4고, v > u의 유량이 3이라면 다음과 같이 표시할 수 있다.  
![image](https://user-images.githubusercontent.com/101376961/165785668-906d0ac9-f36f-48e0-9d38-94acf64b547b.png)  
위 그래프를 다시 양의 순 유량으로 표시하면 다음과 같이 표현할 수 있다.  
![image](https://user-images.githubusercontent.com/101376961/165786370-66ce5291-2149-428a-ac5e-8d56c802086f.png)  
이 과정을  cancellation이라고 한다.  

u에서 v로의 residual capacity cf(u,v)는 다음과 같이 정의된다.  
cf(u,v)=c(u,v)−f(u,v)  

자 그럼 이제 Ford-Fulkerson Algorithm으로 최대 유량을 구해보자.  
먼저 DFS나 BFS로 s에서 t로 가는 경로를 하나 찾는다.  
![image](https://user-images.githubusercontent.com/101376961/165788974-0afce9ad-c391-4110-8f50-b99094282a0b.png)  
이 경우에는 최대 유량은 1이다. 다음으로 위에서 구한 경로의 반대 방향으로 최대 유량만큼 흘려 보내는 엣지를 만들고 s > t 경로를 찾는다.
![image](https://user-images.githubusercontent.com/101376961/165789153-048a830d-0995-47cf-9e76-d6323d1a5cf9.png)  
이 경우에서도 최대 유량은 1이다. 직전 단계에서 구한 경로의 반대 방향으로 최대 유량만큼 흘려 보내는 엣지를 만들고 s > t 경로를 찾는다.  
![image](https://user-images.githubusercontent.com/101376961/165789497-369d3337-0f16-47a1-92fd-f660f28d5750.png)  
이 경우에서도 최대 유량은 1이다. 다시 동일한 엣지를 만들고 s > t 경로를 찾는다.  
![image](https://user-images.githubusercontent.com/101376961/165789767-42d22a42-fe11-4290-90c4-a1b9c830a580.png)
이 경우에서는 최대 유량이 2이다. 이번엔 최대 유량(2)만큼을 흘려 보내는 엣지를 만들고 s > t의 경로를 찾는다. 하지만, 이 경우에 s에서 t로 가는 경로가 더이상 존재하지 않는다. 
![image](https://user-images.githubusercontent.com/101376961/165790011-dadce4cd-6f9a-4d40-ae2d-a4cfb3e7cfaa.png)  
알고리즘을 종료한다. 위 그래프는 residual network 그래프이다. 따라서, s에서 t로 향하는 최대 유량은 a에서 t의 2, b에서 t의 3, 이렇게 해서 총 5가 된다.  
다음은 Ford-Fulkerson 알고리즘의 의사코드이다.  
```
for each edge (u,v) E E[G]
    do f[u,v] <- 0
           f[v,u] <- 0
           
while there exists a path p from s to t in the residual network Gf  
do Cf (p) <- min{Cf (u,v) : (u,v) is in p}  
for each edge (u,v) in p  
      do f[u,v] <- f[u,v] + Cf (p)  
             f[v,u] <- -f[u,v]  
```
이를 C언어를 이용하여 구현해보았다.   
```
#include <stdio.h>

#define A 0
#define B 1
#define C 2
#define MAX_NODES 1000
#define O 1000000000

int n;
int e;
int capacity[MAX_NODES][MAX_NODES];
int flow[MAX_NODES][MAX_NODES];
int color[MAX_NODES];
int pred[MAX_NODES];

int min(int x, int y) {
  return x < y ? x : y;
}

int head, tail;
int q[MAX_NODES + 2];

void enqueue(int x) {
  q[tail] = x;
  tail++;
  color[x] = B;
}

int dequeue() {
  int x = q[head];
  head++;
  color[x] = C;
  return x;
}

// BFS를 사용하여 탐색
int bfs(int start, int target) {
  int u, v;
  for (u = 0; u < n; u++) {
    color[u] = A;
  }
  head = tail = 0;
  enqueue(start);
  pred[start] = -1;
  while (head != tail) {
    u = dequeue();
    for (v = 0; v < n; v++) {
      if (color[v] == A && capacity[u][v] - flow[u][v] > 0) {
        enqueue(v);
        pred[v] = u;
      }
    }
  }
  return color[target] == C;
}

// 알고리즘 적용
int fordFulkerson(int source, int sink) {
  int i, j, u;
  int max_flow = 0;
  for (i = 0; i < n; i++) {
    for (j = 0; j < n; j++) {
      flow[i][j] = 0;
    }
  }

  // 엣지의 residual value 업데이트
  while (bfs(source, sink)) {
    int increment = O;
    for (u = n - 1; pred[u] >= 0; u = pred[u]) {
      increment = min(increment, capacity[pred[u]][u] - flow[pred[u]][u]);
    }
    for (u = n - 1; pred[u] >= 0; u = pred[u]) {
      flow[pred[u]][u] += increment;
      flow[u][pred[u]] -= increment;
    }
    // 해당 경로의 유량 더하기
    max_flow += increment;
  }
  return max_flow;
}

int main() {
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      capacity[i][j] = 0;
    }
  }
  n = 6;
  e = 7;

  capacity[0][1] = 2;
  capacity[0][4] = 3;
  capacity[1][2] = 9;
  capacity[2][4] = 7;
  capacity[2][5] = 3;
  capacity[3][5] = 5;
  capacity[4][2] = 7;
  capacity[4][3] = 8;

  int s = 0, t = 5;
  printf("최대 유량: %d\n", fordFulkerson(s, t));
}
```
실행 결과  
![image](https://user-images.githubusercontent.com/101376961/165793192-36282035-e80c-4900-9e29-b3f107c2083c.png)

