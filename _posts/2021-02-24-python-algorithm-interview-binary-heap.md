---
layout: post
title: 파이썬 알고리즘 인터뷰_이진 힙
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_이진 힙

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 배열에 K번째 큰 요소](#문제01-배열의-K번째-큰-요소)

<br>

##### 문제01 배열에 K번째 큰 요소

-----

> [https://leetcode.com/problems/kth-largest-element-in-an-array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
>
> 정렬되지 않은 배열에서 k번째 큰 요소를 추출하라.
>
> **Example 1:**
>
> ```python
>Input: [3,2,1,5,6,4] and k = 2
> Output: 5
> ```
> 
>    **Example 2:**
>    
>    ```python
>   Input: [3,2,3,1,2,4,5,5,6] and k = 4
>  Output: 4
> ```

<br>

* 풀이1_heapq 모듈 이용

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = list()
        for n in nums:
            heapq.heappush(heap, -n)
        # heap = [-6, -5, -4, -2, -3, -1]
        
        for _ in range(1, k):
            heapq.heappop(heap)
        # heap = [-5, -4, -2, -3, -1]   
        
        return -heapq.heappop(heap)
```

Result

>  Runtime : 68ms, Memory : 15.2MB

<br>

* 풀이2_heapq 모듈의 heapify 이용

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        # nums = [1, 2, 3, 5, 6, 4]
        
        for _ in range(len(nums) - k):
            heapq.heappop(nums)
            
        return heapq.heappop(nums)
```

Result

>  Runtime : 64ms, Memory : 15MB

<br>

* 풀이3_heapq 모듈의 nlargest 이용

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # heapq.nlargest(k, nums) = [6, 5]
        return heapq.nlargest(k, nums)[-1]
```

Result

>  Runtime : 56ms, Memory : 15.1MB

<br>

* 풀이4_정렬을 이용한 풀이

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # sorted(nums, reverse=True) = [6, 5, 4, 3, 2, 1]
        return sorted(nums, reverse=True)[k - 1]
```

Result

>  Runtime : 64ms, Memory : 15.1MB

<br>

