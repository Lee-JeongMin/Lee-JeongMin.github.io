---
layout: post
title: 파이썬 알고리즘 인터뷰_스택 & 큐
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_스택 & 큐

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

스택(stack)

* [문제01 유효한 괄호](#문제01-유효한-괄호)
* [문제02 중복 문자 제거](#문제02-중복-문자-제거)
* [문제03 일일 온도](#문제03-일일-온도) 

큐(queue)

* [문제04 큐를 이용한 스택 구현](#문제04-큐를-이용한-스택-구현)
* [문제05 스택을 이용한 큐 구현](#문제05-스택을-이용한-큐-구현)
* [문제06 원형 큐 디자인](#문제06-원형-큐-디자인)

<br>

##### 연결 리스트를 이용한 스택 ADT 구현

```python
class Node:
    def __init__(self, item, next):
        self.item = item    # 노드의 값
        self.next = next    # 다음 노드를 가리키는 포인터
       
class Stack:
    def __init__(self):
        self.last = None
       
    def push(self, item):
        self.last = Node(item, self.last)
        
    def pop(self):
        item = self.last.item
        self.last = self.last.next
        return item
```

<br>

##### 문제01 유효한 괄호

-----

> [https://leetcode.com/problems/valid-parentheses](https://leetcode.com/problems/valid-parentheses/)
>
> 괄호로 된 입력값이 올바른지 판별하라.
>
> **Example 1:**
>
> ```python
> Input: s = "()"
> Output: true
> ```
>
> **Example 2:**
>
> ```python
> Input: s = "()[]{}"
> Output: true
> ```
>
> **Example 3:**
>
> ```python
> Input: s = "(]"
> Output: false
> ```
>
> **Example 4:**
>
> ```python
> Input: s = "([)]"
> Output: false
> ```
>
> **Example 5:**
>
> ```python
> Input: s = "{[]}"
> Output: true
> ```

<br>

* 풀이1_스택 일치 여부 판별

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        table = {
            ')' : '(',
            '}' : '{',
            ']' : '['
        }
        
        # 스택 이용 예외 처리 및 일치 여부 판별
        for char in s:
            # (,{,[는 스택에 PUSH
            if char not in table:
                stack.append(char)
            # ),},]를 만날 때, 스택에서 POP한 결과가 매핑 테이블의 결과와 동일하는지 판별
            # AND POP한 결과과 일치하지 않거나 스택이 비어있는 경우는 False 리턴
            elif not stack or table[char] != stack.pop():
                return False
        return len(stack) == 0
```

Result

>  Runtime : 32ms, Memory : 14.4MB

<br>

##### 문제02 중복 문자 제거

------

> [https://leetcode.com/problems/remove-duplicate-letters](https://leetcode.com/problems/remove-duplicate-letters/)
>
> 중복된 문자를 제외하고 사전식 순서로 나열하라.
>
> 사전식 순서 : 여러 개의 부분 순서 집합들의 곱집합 위에 존재하는 부분순서를 의미한다.
>
> **Example 1:**
>
> ```
> Input: s = "bcabc"
> Output: "abc"
> ```
> 
>**Example 2:**
> 
>```
> Input: s = "cbacdcbc"
> Output: "acdb"
> ```

<br>

* 풀이1_재귀를 이용한 분리

```python
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        # 집합으로 정렬
        for char in sorted(set(s)):
            suffix = s[s.index(char):]
            # 전체 집합과 접미사 집합이 일치할 때 분리 진행
            if set(s) == set(suffix):
                return char + self.removeDuplicateLetters(suffix.replace(char, ''))  
            
        return ''
                
```

Result

>  Runtime : 88ms, Memory : 14.6MB

<br>

* 풀이2_스택을 이용한 문자 제거

```python
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        counter, seen, stack = collections.Counter(s), set(), []
        
        for char in s:
            counter[char] -= 1
            if char in seen:
                continue
            # 뒤에 붙일 문자가 남아 있다면 스택에서 제거
            while stack and char < stack[-1] and counter[stack[-1]] > 0:
                seen.remove(stack.pop())
            stack.append(char)
            seen.add(char)
            
        return ''.join(stack)
```

Result

>  Runtime : 32ms, Memory : 14.4MB

<br>

##### 문제03 일일 온도

------

> [https://leetcode.com/problems/daily-temperatures](https://leetcode.com/problems/daily-temperatures/)
>
> 매일 화씨 온도(°F) 리스트 T를 입력받아서, 더 따뜻한 날씨를 위해서는 며칠을 더 기다려야 하는지를 출려하라.
>
> **Example 1:**
>
> ```python
> Input: T = [73, 74, 75, 71, 69, 72, 76, 73] 
> Output: [1, 1, 4, 2, 1, 1, 0, 0]
> ```
>

* 풀이1_스택 값 비교

```python
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        answer = [0] * len(T)
        stack = []
        for i, cur in enumerate(T):
            # 현재 온도가 스택 값보다 높다면 정답 처리
            while stack and cur > T[stack[-1]]:
                last = stack.pop()
                answer[last] = i - last
            stack.append(i)
        
        return answer
```

Result

>  Runtime : 492ms, Memory : 18.8MB

<br>

##### 문제04 큐를 이용한 스택 구현

------

> [https://leetcode.com/problems/implement-stack-using-Queues](https://leetcode.com/problems/implement-stack-using-Queues/)
>
> 큐를 이용해 다음 연산을 지원하는 스택을 구현하라.
>
> * push(x) : 요소 x를 스택에 삽입한다. 
> * pop() : 스택의 첫 번째 요소를 삭제한다.
> * top() : 스택의 첫 번째 요소를 가져온다.
> * empty() : 스택이 비어 있는지 여부를 리턴한다.
>
> **Example 1:**
>
> ```python
> Input
> ["MyStack", "push", "push", "top", "pop", "empty"]
> [[], [1], [2], [], [], []]
> Output
> [null, null, null, 2, 2, false]
> 
> Explanation
> MyStack myStack = new MyStack();
> myStack.push(1);
> myStack.push(2);
> myStack.top(); // return 2
> myStack.pop(); // return 2
> myStack.empty(); // return False
> ```

<br>

* 내 풀이

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.q = collections.deque()
        

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        self.q.appendleft(x)
        

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        return self.q.popleft()
        

    def top(self) -> int:
        """
        Get the top element.
        """
        return self.q[0]
        

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return len(self.q) == 0
```

Result

>  Runtime : 24ms, Memory : 14.4MB

<br>

* 풀이1_push() 할 때 큐를 이용해 재정렬

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.q = collections.deque()
        

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        self.q.append(x)
        # 요소 삽입 후 맨 앞에 두는 상태로 재정렬(스택은 LIFO이기 때문)
        for _ in range(len(self.q) - 1):
            self.q.append(self.q.popleft())
        

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        return self.q.popleft()
        

    def top(self) -> int:
        """
        Get the top element.
        """
        return self.q[0]
        

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return len(self.q) == 0
```

Result

>  Runtime : 56ms, Memory : 14.3MB

<br>

##### 문제05 스택을 이용한 큐 구현

------

> [https://leetcode.com/problems/implement-queue-using-stacks](https://leetcode.com/problems/implement-queue-using-stacks/)
>
> 스택을 이용해 다음 연산을 지원하는 큐를 구현하라.
>
> * push(x) : 요소 x를 큐 마지막에 삽입한다.
> * pop() : 큐 처음에 있는 요소를 제거한다.
> * peek() : 큐 처음에 있는 요소를 조회한다.
> * emtpy() : 큐가 비어 있는지 여부를 리턴한다.
>
> **Example:**
>
> ```python
> Input
> ["MyQueue", "push", "push", "peek", "pop", "empty"]
> [[], [1], [2], [], [], []]
> Output
> [null, null, null, 1, 1, false]
> 
> Explanation
> MyQueue myQueue = new MyQueue();
> myQueue.push(1); // queue is: [1]
> myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
> myQueue.peek(); // return 1
> myQueue.pop(); // return 1, queue is [2]
> myQueue.empty(); // return false
> ```

<br>

* 내 풀이

```python
class MyQueue:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack = []

    def push(self, x: int) -> None:
        """
        Push element x to the back of queue.
        """
        self.stack.append(x)
        

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        pop_ele = self.stack[0]
        self.stack = self.stack[1:]
        return pop_ele
        

    def peek(self) -> int:
        """
        Get the front element.
        """
        return self.stack[0]
        

    def empty(self) -> bool:
        """
        Returns whether the queue is empty.
        """
        return len(self.stack) == 0
```

Result

> Runtime : 32ms, Memory : 14.4MB

<br>

* 풀이1_스택 2개 사용

```python
class MyQueue:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.input = []
        self.output = []
        
    def push(self, x: int) -> None:
        """
        Push element x to the back of queue.
        """
        self.input.append(x)
        

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        self.peek()
        return self.output.pop()
        

    def peek(self) -> int:
        """
        Get the front element.
        """
        # output이 없으면 모두 재입력
        if not self.output:
            while self.input:
                self.output.append(self.input.pop())
        return self.output[-1]
        

    def empty(self) -> bool:
        """
        Returns whether the queue is empty.
        """
        return self.input == [] and self.output == []
```

Result

> Runtime : 28ms, Memory : 14.1MB

<br>

##### 문제06 원형 큐 디자인

------

> [https://leetcode.com/problems/design-circular-queue](https://leetcode.com/problems/design-circular-queue/)
>
> 원형 큐를 디자인하라.
>
> **Example 1:**
>
> ```python
> Input
> ["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
> [[3], [1], [2], [3], [4], [], [], [], [4], []]
> Output
> [null, true, true, true, false, 3, true, true, true, 4]
> 
> Explanation
> MyCircularQueue myCircularQueue = new MyCircularQueue(3);
> myCircularQueue.enQueue(1); // return True
> myCircularQueue.enQueue(2); // return True
> myCircularQueue.enQueue(3); // return True
> myCircularQueue.enQueue(4); // return False
> myCircularQueue.Rear();     // return 3
> myCircularQueue.isFull();   // return True
> myCircularQueue.deQueue();  // return True
> myCircularQueue.enQueue(4); // return True
> myCircularQueue.Rear();     // return 4
> ```
>

<br>

* 풀이1_배열을 이용한 풀이

```python
class MyCircularQueue:

    def __init__(self, k: int):
        # 큐의 크기 : k
        self.q = [None]* k
        self.maxlen = k
        # front 포인터
        self.p1 = 0
        # rear 포인터
        self.p2 = 0

    # enQueue() : rear 포인터 이동
    def enQueue(self, value: int) -> bool:
        '''요소 삽입''' 
        if self.q[self.p2] is None:
            # rear 포인터 p2위치에 삽입될 값을 넣는다.
            self.q[self.p2] = value
            # rear 포인터는 한 칸 앞으로 이동한다.(전체 길이만큼 나머지 연산을 통해 포인터의 위치가 전체 길이를 넘어가지 않도록 함)
            self.p2 = (self.p2 + 1) % self.maxlen
            return True
        else:
            return False

    # deQueue() : front 포인터 이동    
    def deQueue(self) -> bool:
        '''요소 삭제(요소 추출하지 않고 삭제만 진행)'''
        if self.q[self.p1] is None:
            return False
        else:
            # front 포인터에 None를 넣어 값을 삭제한다.
            self.q[self.p1] = None
            # 포인터를 한 칸 앞으로 이동하며 전체 길이를 넘지 않도록 한다.
            self.p1 = (self.p1 + 1) % self.maxlen
            return True

    def Front(self) -> int:
        return -1 if self.q[self.p1] is None else self.q[self.p1]

    def Rear(self) -> int:
        return -1 if self.q[self.p2 - 1] is None else self.q[self.p2 -1]

    def isEmpty(self) -> bool:
        return self.p1 == self.p2 and self.q[self.p1] is None

    def isFull(self) -> bool:
        return self.p1 == self.p2 and self.q[self.p1] is not None
```

Result

> Runtime : 68ms, Memory : 14.9MB
>

<br>

##### 원형 큐(Circular Queue)

큐를 위해 배열을 지정해 놓고 쓰다보면 배열의 앞 부분이 비게된다는 점을 활용해서 배열의 맨 마지막 부분을 쓰면 다시 제일 처음부터 다시 큐를 채우는 형태의 큐이다.

![circular_queue]({{ site.baseurl }}/assets/img/circular_queue.png)

동작 원리는 투 포인터와 비슷하다. 마지막 위치와 시작 위치를 연결하는 원형 구조를 만든 후, 요소의 시작점과 끝점을 따라 투 포인터가 움직인다. enQueue()를 하게 되면 rear 포인터가 앞으로 이동하고, deQueue()를 하게 되면 front 포인터가 앞으로 이동하는 방식이다.