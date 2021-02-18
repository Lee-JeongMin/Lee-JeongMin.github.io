---
layout: post
title: 파이썬 알고리즘 인터뷰_최단 경로
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_최단 경로

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 네트워크 딜레이 타임](#문제01-네트워크-딜레이-타임)
* [문제02 K 경유지 내 가장 저렴한 항공권](#문제02-K-경유지-내-가장-저렴한-항공권)

<br>

##### 문제01 네트워크 딜레이 타임

-----

> [https://leetcode.com/problems/network-delay-time](https://leetcode.com/problems/network-delay-time/)
>
> K부터 출발해 모든 노드가 신호를 받을 수 있는 시간을 계산하라. 불가능할 경우 -1을 리턴한다. 입력값 (u, v, w)는 각각 출발지, 도착지, 소요 시간으로 구성되며, 전체 노드의 개수는 N으로 입력받는다.
>
> **Example 1:**
>
> ![img]({{ site.baseurl }}/assets/img/931_example_1.png)
>
> ```python
>Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
> Output: 2
> ```
>   
>   **Example 2:**
>   
>   ```python
> Input: times = [[1,2,1]], n = 2, k = 1
> Output: 1
> ```
>
> **Example 3:**
>
> ```python
> Input: times = [[1,2,1]], n = 2, k = 2
>   Output: -1
>   ```

<br>

* 풀이1_다익스트라 알고리즘 구현

```python
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = collections.defaultdict(list)
        # 그래프 인접 리스트 구성
        for u, v, w in times:
            graph[u].append((v,w))
            
        # 큐 변수 : [(소요 시간, 정점)]
        Q = [(0, k)]
        dist = collections.defaultdict(list)
        
        # 우선순위 큐 최솟값 기준으로 정점까지 최단 경로 삽입
        while Q:
            time, node = heapq.heappop(Q)
            if node not in dist:
                dist[node] = time
                for v, w in graph[node]:
                    alt = time + w
                    heapq.heappush(Q, (alt, v))
                    
        # 모든 노드의 최단 경로 존재 여부 판별
        if len(dist) == n:
            return max(dist.values())
        return -1
```

Result

>  Runtime : 488ms, Memory : 16.1MB

<br>

##### 문제02 K 경유지 내 가장 저렴한 항공권

------

> [https://leetcode.com/problems/cheapest-flights-within-k-stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
>
> 시작점에서 도착점까지 가장 저렴한 가격을 계산하되, K개의 경유지 이내에 도착하는 가격을 리턴하라. 경로가 존재하지 않을 경우 -1을 리턴한다.
>
> **Example 1:**
>
> <img src="{{ site.baseurl }}/assets/img/995.png" alt="img" style="zoom:43%;" />
>
> ```python
> Example 1:
> Input: 
> n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
> src = 0, dst = 2, k = 1
> Output: 200
> Explanation: 
> The graph looks like this:
> The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.
> ```
>
> **Example 2:**
>
> <img src="{{ site.baseurl }}/assets/img/995.png" alt="img" style="zoom:43%;" />
>
> ```python
> Input: 
> n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
> src = 0, dst = 2, k = 0
> Output: 500
> Explanation: 
> The graph looks like this:
> The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.
> ```
>

<br>

* 풀이1_다익스트라 알고리즘 응용

```python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        graph = collections.defaultdict(list)
        # 그래프 인접 리스트 구성
        for u, v, w in flights:
            graph[u].append((v,w))
            
        # 큐 변수 : [(가격, 정점, 남은 가능 경유지 수)]
        Q = [(0, src, K)]
        
        # 우선순위 큐 최솟값 기준으로 도착점까지 최소 비용 판별
        while Q:
            price, node, k = heapq.heappop(Q)
            if node == dst:
                return price
            if k>= 0:
                for v, w in graph[node]:
                    alt = price + w
                    heapq.heappush(Q, (alt, v, k - 1))
        
        return -1
```

Result

>  Runtime : 92ms, Memory : 19.9MB

<br>