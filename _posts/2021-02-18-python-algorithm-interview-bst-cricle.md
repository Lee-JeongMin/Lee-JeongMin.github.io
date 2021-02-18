---
layout: post
title: 파이썬 알고리즘 인터뷰_이진 트리
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_이진 트리

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 정렬된 배열의 이진 탐색 트리 변환](#문제01-정렬된-배열의-이진-탐색-트리-변환)
* [문제02 이진 탐색 트리(BST)를 더 큰 수 합계 트리로](#문제02-이진-탐색-트리(BST)를-더-큰-수-합계-트리로)
* [문제03 이진 탐색 트리(BST) 합의 범위](#문제03-이진-탐색-트리(BST)-합의-범위)
* [문제04 이진 탐색 트리(BST) 노드 간 최소 거리](#문제04-이진-탐색-트리(BST)-노드-간-최소-거리)
* [문제05 전위, 중위 순회 결과로 이진 트리 구축](# 문제05-전위,-중쥐-순회-결과로-이진-트리-구축)

<br>

##### 문제01 정렬된 배열의 이진 탐색 트리 변환

-----

> [https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
>
> 오름차순으로 정렬된 배열을 높이 균형 이진 탐색 트리로 변환하라.
>
> **Example:**
>
> ```python
>Given the sorted array: [-10,-3,0,5,9],
> 
> One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
> 
>       0
>     / \
>    -3   9
>   /   /
>  -10  5
> ```

<br>

* 풀이1_이진 검색 결과로 트리 구성

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None
        
        mid = len(nums) // 2
        
        # 분할 정복으로 이진 검색 결과 트리 구성
        node = TreeNode(nums[mid])
        node.left = self.sortedArrayToBST(nums[:mid])
        node.right = self.sortedArrayToBST(nums[mid + 1 :])
        
        return node
```

Result

>  Runtime : 76ms, Memory : 16.6MB

<br>

##### 문제02 이진 탐색 트리(BST)를 더 큰 수 합계 트리로

------

> [https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/)
>
> BST의 각 노드를 현재값보다 더 큰 값을 가진 모든 노드의 합으로 만들어라.
>
> 

<br>

* 풀이1_중위 순회로 노드 값 누적

```python

```

Result

>  Runtime : 36ms, Memory : 16.4MB

<br>

##### 문제03 이진 탐색 트리(BST) 합의 범위

------

> [https://leetcode.com/problems/range-sum-of-bst](https://leetcode.com/problems/range-sum-of-bst/)
>
> 이진 탐색 트리(BST)가 주어졌을 때 L 이상 R 이하의 값을 지닌 노드의 합을 구하라.
>
> 

<br>

* 풀이1_재귀 구조 DFS로 브루트 포스 탐색

```python

```

Result

>  Runtime : 392ms, Memory : 17.9MB

<br>

* 풀이2_DFS 가지치기로 필요한 노드 탐색

```python

```

Result

>  Runtime : 392ms, Memory : 17.9MB

<br>

* 풀이3_반복 구조 DFS로 필요한 노드 탐색

```python

```

Result

>  Runtime : 392ms, Memory : 17.9MB

<br>

* 풀이4_반복 구조 BFS로 필요한 노드 탐색

```python

```

Result

>  Runtime : 392ms, Memory : 17.9MB

<br>

##### 문제04 이진 탐색 트리(BST) 노드 간 최소 거리

------

> [https://leetcode.com/problems/minimum-distance-between-bst-nodes](https://leetcode.com/problems/minimum-distance-between-bst-nodes/)
>
> 두 노드 간 값의 차이가 가장 작은 노드의 값의 차이를 출력하라.
>
> 
>

<br>

* 풀이1_재귀 구조로 중위 순회

```python

```

Result

>  Runtime : 32ms, Memory : 14.3MB

<br>

* 풀이2_반복 구조로 중위 순회

```python

```

Result

>  Runtime : 32ms, Memory : 14.3MB

<br>

##### 문제05 전위, 중위 순회 결과로 이진 트리 구축

------

> [https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
>
> 트리의 전위, 중위 순회 결과를 입력값으로 받아 이진 트리를 구축하라.
>
> 
>

<br>

* 풀이1_전위 순회 결과로 중위 순회 분할 정복

```python

```

Result

>  Runtime : 72ms, Memory : 15.3MB

<br>