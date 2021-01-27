---
layout: post
title: 파이썬 알고리즘 인터뷰_데크 & 우선순위 큐
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_데크 & 우선순위 큐

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

데크(deque)

* [문제01 원형 데크 디자인](#문제01-원형-데크-디자인)

큐(queue)

* [문제02 k개 정렬 리스트 병합](#문제02-k개-정렬-리스트-병합)

<br>

##### 문제01 원형 데크 디자인

-----

> [https://leetcode.com/problems/design-circular-deque](https://leetcode.com/problems/design-circular-deque/)
>
> 다음 연산을 제공하는 원형 데크를 디자인하라.
>
> * MyCircularDeque(k) : 데크 사이즈를 k로 지정하는 생성자다.
>* insertFront() : 데크 처음에 아이템을 추가하고 성공할 경우 true를 리턴한다.
> * insertLast() : 데크 마지막에 아이템을 추가하고 성공할 경우 true를 리턴한다.
> * deleteFront() : 데크 처음에 아이템을 삭제하고 성공할 경우 true를 리턴한다.
> * deleteLast() : 데크 마지막에 아이템을 삭제하고 성공할 경우 true를 리턴한다.
> * getFront() : 데크의 첫 번째 아이템을 가져온다. 데크가 비어 있다면 -1을 리턴한다.
>* getRear() : 데크의 마지막 아이템을 가져온다. 데크가 비어 있다면 -1을 리턴한다.
> * isEmpty() : 데크가 비어 있는지 여부를 판별한다.
>* isFull() : 데크가 가득 차 있는지 여부를 판별한다.
> 
> **Example 1:**
> 
> ```python
>MyCircularDeque circularDeque = new MycircularDeque(3); // set the size to be 3
> circularDeque.insertLast(1);			// return true
>circularDeque.insertLast(2);			// return true
> circularDeque.insertFront(3);			// return true
> circularDeque.insertFront(4);			// return false, the queue is full
> circularDeque.getRear();  			// return 2
> circularDeque.isFull();				// return true
>circularDeque.deleteLast();			// return true
> circularDeque.insertFront(4);			// return true
>circularDeque.getFront();			// return 4
> ```
> 

<br>

* 풀이1_이중 연결 리스트를 이용한 데크 구현

```python
class MyCircularDeque:

    def __init__(self, k: int):
        """
        Initialize your data structure here. Set the size of the deque to be k.
        """
        self.head, self.tail = ListNode(None), ListNode(None)
        # 최대 길이, 현재 길이
        self.k, self.len = k, 0
        self.head.right, self.tail.left = self.tail, self.head

        # 이중 연결 리스트에 신규 노드 삽입
        # 이미 있는 노드를 찢어내고 그 사이에 새로운 노드 new를 삽입하는 형태
    def _add(self, node: ListNode, new: ListNode):
        n = node.right
        node.right = new
        new.left, new.right = node, n
        n.left = new
    
    def _del(self, node:ListNode):
        n = node.right.right
        node.right = n
        n.left = node

    def insertFront(self, value: int) -> bool:
        """
        Adds an item at the front of Deque. Return true if the operation is successful.
        """
        # 이미 꽉 차있는 경우 False 반환
        if self.len == self.k:
            return False
        self.len += 1
        # head 위치에 노드 삽입
        self._add(self.head, ListNode(value))
        return True

    def insertLast(self, value: int) -> bool:
        """
        Adds an item at the rear of Deque. Return true if the operation is successful.
        """
        if self.len == self.k:
            return False
        self.len += 1
        # tail.left에 노드 삽입
        self._add(self.tail.left, ListNode(value))
        return True

    def deleteFront(self) -> bool:
        """
        Deletes an item from the front of Deque. Return true if the operation is successful.
        """
        if self.len == 0:
            return False
        self.len -= 1
        self._del(self.head)
        return True
        

    def deleteLast(self) -> bool:
        """
        Deletes an item from the rear of Deque. Return true if the operation is successful.
        """
        if self.len == 0:
            return False
        self.len -= 1
        self._del(self.tail.left.left)
        return True

    def getFront(self) -> int:
        """
        Get the front item from the deque.
        """
        return self.head.right.val if self.len else -1
        

    def getRear(self) -> int:
        """
        Get the last item from the deque.
        """
        return self.tail.left.val if self.len else -1

    def isEmpty(self) -> bool:
        """
        Checks whether the circular deque is empty or not.
        """
        return self.len == 0

    def isFull(self) -> bool:
        """
        Checks whether the circular deque is full or not.
        """
        return self.len == self.k
```

Result

>  Runtime : 108ms, Memory : 15.5MB

<br>

##### 우선순위 큐

> 우선순위 큐는 큐 또는 스택과 같은 추상 자료형과 유사하지만 추가로 각 요소의 '우선순위'와 연관되어 있다.

<br>

##### 문제02 k개 정렬 리스트 병합

------

> [https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)
>
> k개의 정렬된 리스트를 1개의 정렬된 리스트로 병합하라.
>
> **Example 1:**
>
> ```python
> Input: lists = [[1,4,5],[1,3,4],[2,6]]
> Output: [1,1,2,3,4,4,5,6]
> Explanation: The linked-lists are:
> [
>   1->4->5,
>   1->3->4,
>   2->6
> ]
> merging them into one sorted list:
> 1->1->2->3->4->4->5->6
> ```
>
> **Example 2:**
>
> ```python
> Input: lists = []
> Output: []
> ```
>
> **Example 3:**
>
> ```python
> Input: lists = [[]]
> Output: []
> ```

<br>

* 풀이1_우선순위 큐를 이용한 리스트 병합

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        root = result = ListNode(None)
        heap = []
        
        # 각 연결 리스트의 루트를 힙에 저장
        for i in range(len(lists)):
            if lists[i]:
                heapq.heappush(heap, (lists[i].val, i, lists[i]))
            
        # 힙 추출 이후 다음 노드는 다시 저장
        while heap:
            node = heapq.heappop(heap)
            idx = node[1]
            result.next = node[2]
            
            result = result.next
            if result.next:
                heapq.heappush(heap, (result.next.val, idx, result.next))
                
        return root.next
```

Result

>  Runtime : 96ms, Memory : 18MB

<br>

##### PriorityQueue vs heapq

파이썬의 우선순위 큐는 queue 모듈의 PriorityQueue클래스를 이용해 사용할 수 있다. 하지만 우선순위 큐는 주로 힙을 사용해 구현한다.

 PriorityQueue와 heapq의 차이점은 무엇일까? 스레드 세이프(Thread-Safe)이다. 하지만 파이썬에서는 멀티 스레딩이 거의 의미가 없기 때문에 PriorityQueue를 사용할 필요가 없다. 

