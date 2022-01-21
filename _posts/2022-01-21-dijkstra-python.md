---
published: true
title:  "[Algorithm] 다익스트라(Dijkstra) 구현 (Python)"
excerpt: "다익스트라 알고리즘을 파이썬으로 구현해 보자"

categories:
  - Algorithm
tags:
  - [다익스트라, Python]

toc: true
toc_sticky: true
 
date: 2022-01-21
last_modified_at: 2022-01-21
---
<br>

> ❗ 이 포스트는 다익스트라 알고리즘을 알고 있다는 전제 하에 작성되었습니다. 다익스트라를 파이썬으로 어떻게 구현할까에 대한 글 입니다 🙇‍♀️

# 다익스트라 의사 코드
출처 : [위키피디아](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98#%EC%9D%98%EC%82%AC_%EC%BD%94%EB%93%9C)
```text
function Dijkstra(Graph, source):
    dist[source] ← 0                                    // 초기화

    create vertex set Q

    for each vertex v in Graph:    // 초기화
        if v ≠ source
            dist[v] ← INFINITY                          // 소스에서 v까지의 아직 모르는 길이
            prev[v] ← UNDEFINED                             // v의 이전 노드

            Q.add_with_priority(v, dist[v])
    
     while Q is not empty:                          // 메인 루프
        u ← Q.extract_min()                         // 최고의 꼭짓점을 제거하고 반환한다
        for each neighbor v of u:              // Q에 여전히 남아 있는 v에 대해서만
            alt ← dist[u] + length(u, v)
            if alt < dist[v]
                dist[v] ← alt
                prev[v] ← u
                Q.decrease_priority(v, alt)

    return dist, prev
```

# 파이썬으로 구현하기

먼저 그래프는 이렇게 구성한다.
```python
# ------- 입력 받기 시작 ------
N = int(input()) # 노드 갯수
M = int(input()) # 간선 갯수

graph = collections.defaultdict(list)

for _ in range(M):
    # 출발, 도착, 가중치
    u, v, w = map(int, input().split())
    graph[u].append((v, w))

start = int(input())
# ------- 입력 받기 끝 ------

dist = collections.defaultdict(int) # 거리
```
`collections.defaultdict`를 이용해 해당 키가 존재하지 않을 경우에도 따로 if문을 통한 검사 없이 삽입할 수 있도록 한다.

key로 출발노드, value로 (도착노드, 가중치) 를 갖는다.

dist도 똑같이 `collections.defaultdict`를 이용하고 기본값은 `int` 이다.

```python
Q = [(0, start)]
```
큐 변수 Q는 (가중치, 정점) 으로 구성한다.

처음 시작점이므로 (0, start)를 큐에 삽입해준다.

다음으로 Q를 순회하면서 가중치가 작은 정점을 차례로 방문하며 총 소요된 가중치의 합을 구한다.

최소힙을 사용하기 위해서 파이썬의 `heapq`를 사용했다. 파이썬에도 PriorityQueue가 있지만, 파이썬의 우선순위큐는 사실 내부적으로 `heapq`로 구현되어 있어 보통 `heapq`를 사용한다.

위의 의사코드에서는 아직 모르는 길이를 무한대로 설정하고 거리를 비교하며 갱신해 나갔다. 그리고 뒤에선 `Q.decrease_priority`를 이용해 우선순위를 조정하는데 파이썬의 `heapq`에는 그러한 기능이 없다.

따라서 `Q.decrease_priority` 가 필요 없도록 구현 해야한다.

```python
while Q:
    # 가중치 가장 적은것 pop, Q최소힙
    time, node = heapq.heappop(Q)
    # 해당 노드에 처음 방문 할 때에만
    if node not in dist:
        dist[node] = time
        for v, w in graph[node]:
            alt = time + w
            heapq.heappush(Q, (alt, v))
```

큐 순회를 시작하자마자 최솟값을 추출하는것은 의사코드와 동일하다. `Q.extract_min()`을 `heapq.heappop(Q)`가 대신한다.

의사코드에서는 최솟값을 추출하고 이웃 노드를 순회하는 반면 우리는 먼저 dist에 node가 포함되어 있는지 검사한다.

의사코드에선 dist를 무한대로 초기화 시켜놓았지만 우리는 아직 방문하지 않은 노드는 비어있는 상태이다.

따라서 `dist[node]` 값이 비어있을 때에만 큐에 push 한다. 이렇게 되면 dist에는 항상 최솟값만 셋팅된다.

<hr>

모든 작업이 끝나게 되면 dist 딕셔너리에 모든 노드에 대한 최단 경로가 들어있을것이다. 만약 키의 갯수가 노드의 갯수와 동일하지 않다면 그 노드는 시작점에서 갈 수 없는 노드인것이다.

[백준 1916 최소비용 구하기](https://devyuseon.github.io/boj/boj-1916/) 에서는 출발점에서 도착점을 갈 수 있는 경우만 입력으로 주어진다고 했으니 길이를 검사하지 않는다.

끝부분의 처리는 문제마다 다르므로 잘 살펴봐야 한다.


# 전체 소스코드

```python
import sys
import collections
import heapq
input = sys.stdin.readline

def dijkstra(start):
    # (가중치, 정점)
    Q = [(0, start)]

    while Q:
        # 가중치 가장 적은것 pop, Q최소힙
        time, node = heapq.heappop(Q)
        # 해당 노드에 처음 방문 할 때에만
        if node not in dist:
            dist[node] = time
            for v, w in graph[node]:
                alt = time + w
                heapq.heappush(Q, (alt, v))

# ------- 입력 받기 시작 ------
N = int(input()) # 노드 갯수
M = int(input()) # 간선 갯수

graph = collections.defaultdict(list)

for _ in range(M):
    # 출발, 도착, 가중치
    u, v, w = map(int, input().split())
    graph[u].append((v, w))

start = int(input())
# ------- 입력 받기 끝 ------

dist = collections.defaultdict(int) # 거리
dijkstra(start)

for k, v in dist.items():
    print(f"노드: {k}, 거리: {v}")
```

**입력**
```text
5
8
1 2 2
1 3 3
1 4 1
1 5 10
2 4 2
3 4 1
3 5 1
4 5 3
1
```

**출력**
```text
노드: 1, 거리: 0
노드: 4, 거리: 1
노드: 2, 거리: 2
노드: 3, 거리: 3
노드: 5, 거리: 4
```