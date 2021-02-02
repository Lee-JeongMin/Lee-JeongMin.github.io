---
layout: post
title: 파이썬 알고리즘 인터뷰_그래프
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_그래프

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 섬의 개수](#문제01-섬의-개수)
* [문제02 전화 번호 문자 조합](#문제02-전화-번호-문자-조합)
* [문제03 중복 문자 없는 가장 긴 부분 문자열](#문제03-중복-문자-없는-가장-긴-부분-문자열)
* [문제04 상위 K 빈도 요소](#문제04-상위-K-빈도-요소)
* [문제05 해시맵 디자인](#문제01-해시맵-디자인)
* [문제06 보석과 돌](#문제02-보석과-돌)
* [문제07 중복 문자 없는 가장 긴 부분 문자열](#문제03-중복-문자-없는-가장-긴-부분-문자열)
* [문제08 상위 K 빈도 요소](#문제04-상위-K-빈도-요소)

<br>

##### 문제01 해시맵 디자인

-----

> [https://leetcode.com/problems/design-hashmap](https://leetcode.com/problems/design-hashmap/)
>
> 다음의 기능을 제공하는 해시맵을 디자인하라.
>
> * put(key, value) : 키, 값을 해시맵에 삽입한다. 만약 이미 존재하는 키하면 업데이트한다.  
> * get(key) : 키에 해당되는 값을 조회한다. 만약 키가 존재하지 않는다면 -1을 리턴한다.
> * remove(key) :키에 해당하는 키,값을 해시맵에서 삭제한다.
>
> **Example 1:**
>
> ```python
> MyHashMap hashMap = new MyHashMap();
> hashMap.put(1, 1);          
> hashMap.put(2, 2);         
> hashMap.get(1);            // returns 1
> hashMap.get(3);            // returns -1 (not found)
> hashMap.put(2, 1);          // update the existing value
> hashMap.get(2);            // returns 1 
> hashMap.remove(2);          // remove the mapping for 2
> hashMap.get(2);            // returns -1 (not found) 
> ```
>

<br>

* 풀이1_개별 체이닝 방식을 이용한 해시 테이블 구현

```python
class ListNode:
    def __init__(self, key=None, value=None):
        self.key = key
        self.value = value
        self.next = None
        
class MyHashMap:

    def __init__(self):
        # 초기화
        self.size = 1000
        self.table = collections.defaultdict(ListNode)

    def put(self, key: int, value: int) -> None:
        # 제산법 사용
        index = key % self.size
        
        # 인덱스에 노드가 없다면 삽입 후 종료
        if self.table[index].value is None:
            self.table[index] = ListNode(key, value)
            return
        
        # 인덱스에 노드가 존재하는 경우 연결 리스트 처리(개별 체이닝)
        p = self.table[index]
        while p:
            if p.key == key:
                p.value = value
                return
            if p.next is None:
                break
            p = p.next
        p.next = ListNode(key, value)

    # 조회
    def get(self, key: int) -> int:
        index = key % self.size
        if self.table[index].value is None:
            return -1
        
        # 노드가 존재할 때 일치하는 키 탐색
        p = self.table[index]
        while p:
            if p.key == key:
                return p.value
            p = p.next
        return -1
        
    # 삭제
    def remove(self, key: int) -> None:
        index = key % self.size
        if self.table[index].value is None:
            return
        
        # 인덱스의 첫 번째 노드일때 삭제 처리
        p = self.table[index]
        if p.key == key:
            self.table[index] = ListNode() if p.next is None else p.next
            return
        # 연결 리스트 노드 삭제
        prev = p
        while p:
            if p.key == key:
                prev.next = p.next
                return
            prev, p = p, p.next

```

Result

>  Runtime : 220ms, Memory : 17.4MB

<br>

##### 문제02 보석과 돌

------

> [https://leetcode.com/problems/jewels-and-stones](https://leetcode.com/problems/jewels-and-stones/)
>
> J는 보석이며, S는 갖고 있는 돌이다. S에는 보석이 몇 개나 있을까? 대소문자는 구분한다.
>
> **Example 1:**
>
> ```python
> Input: jewels = "aA", stones = "aAAbbbb"
> Output: 3
> ```
> 
>   **Example 2:**
>   
>   ```python
> Input: jewels = "z", stones = "ZZ"
> Output: 0
> ```
> 

<br>

* 내 풀이 & 풀이3_Counter로 계산 생략

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        _sum = 0
        cnt = collections.Counter(stones)

        for j in jewels:
            _sum += cnt[j]

        return _sum
```

Result

>  Runtime : 32ms, Memory : 14.1MB

<br>

* 풀이1_해시 테이블을 이용한 풀이

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        freqs = {}
        count = 0
        
        # 돌(stones)의 빈도수 계산
        for char in stones:
            if char not in freqs:
                freqs[char] = 1
            else:
                freqs[char] += 1
        
        # 보석(jewels)의 빈도수 합산
        for char in jewels:
            if char in freqs:
                count += freqs[char]
        
        return count
```

Result

>  Runtime : 24ms, Memory : 14.3MB

<br>

* 풀이2_defaultdict를 이용한 비교 생략

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        freqs = collections.defaultdict(int)
        count = 0
        
        # 비교 없이 돌(stones)의 빈도수 계산
        for char in stones:
            freqs[char] += 1
        
        # 비교 없이 보석(jewels)의 빈도수 합산
        for char in jewels:
                count += freqs[char]
        
        return count
```

Result

>  Runtime : 32ms, Memory : 14.4MB

<br>

* 풀이4_파이썬다운 방식

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        return sum(s in jewels for s in stones)
```

Result

>  Runtime : 28ms, Memory : 14.3MB

<br>

##### 문제03 중복 문자 없는 가장 긴 부분 문자열

------

> [https://leetcode.com/problems/longest-substring-without-repeating-characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
>
> 중복 문자가 없는 가장 긴 부분 문자열의 길이를 리턴하라.
>
> **Example 1:**
>
> ```python
> Input: s = "abcabcbb"
> Output: 3
> Explanation: The answer is "abc", with the length of 3.
> ```
>
> **Example 2:**
>
> ```python
> Input: s = "bbbbb"
> Output: 1
> Explanation: The answer is "b", with the length of 1.
> ```
>
> **Example 3:**
>
> ```python
> Input: s = "pwwkew"
> Output: 3
> Explanation: The answer is "wke", with the length of 3.
> Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
> ```
>
> **Example 4:**
>
> ```python
> Input: s = ""
> Output: 0
> ```

<br>

* 풀이1_슬라이딩 윈도우와 투 포인터로 사이즈 조절

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        used = {}
        max_length = start = 0
        for index, char in enumerate(s):
            # 이미 등장했던 문자라면 'start'위치 갱신
            if char in used and start <= used[char]:
                start = used[char] + 1
            else:  # 최대 부분 문자열 길이 갱신
                max_length = max(max_length, index - start + 1)
            
            # 현재 문자의 위치 삽입
            used[char] = index
        
        return max_length
```

Result

>  Runtime : 48ms, Memory : 14.3MB

<br>

##### 문제04 상위 K 빈도 요소

------

> [https://leetcode.com/problems/top-k-frequent-elements](https://leetcode.com/problems/top-k-frequent-elements/)
>
> k번 이상 등장하는 요소를 추출하라.( = 빈도 상위 k개 요소 추출 )
>
> **Example 1:**
>
> ```python
> Input: nums = [1,1,1,2,2,3], k = 2
> Output: [1,2]
> ```
>
> **Example 2:**
>
> ```python
> Input: nums = [1], k = 1
> Output: [1]
> ```

* 내 코드

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        freqs = collections.Counter(nums)
        most = freqs.most_common(k)
        return [key for key, val in most]
```

Result

>  Runtime : 108ms, Memory : 18.6MB

<br>

* 풀이1_Counter를 이용한 음수 순 추출

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        freqs_heap = []
        freqs = collections.Counter(nums)
        # 힙에 음수로 삽입
        for f in freqs:
            heapq.heappush(freqs_heap, (-freqs[f], f))
            
        topk = list()
        # k번 만큼 추출, 최소 힙(Min Heap)이므로 가장 작은 음수 순으로 추출
        for _ in range(k):
            topk.append(heapq.heappop(freqs_heap)[1])
        
        return topk
```

Result

>  Runtime : 92ms, Memory : 18.8MB

<br>

* 풀이2_파이썬다운 방식

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        return list(zip(*collections.Counter(nums).most_common(k)))[0]
```

Result

>  Runtime : 112ms, Memory : 18.6MB

<br>

##### zip() 함수

> zip() 함수는 2개 이상의 시퀀스를 짧은 길이를 기준으로 일대일 대응하는 새로운 튜플 시퀀스를 만드는 역할

```python
a = [1, 2, 3, 4]
b = ['a', 'b', 'c', 'd']
c = ['ㄱ', 'ㄴ', 'ㄷ', 'ㄹ']
list(zip(a,b,c))

# [(1, 'a', 'ㄱ'), (2, 'b', 'ㄴ'), (3, 'c', 'ㄷ'), (4, 'd', 'ㄹ')]
```

<br>

##### 아스테리스크(*)

> 언팩(Unpack) 역할을 한다. 주로 튜플이나 리스트를 언패킹(풀어 헤치는 데) 사용한다.

```python
fruits = ['lemon', 'pear', 'watermelon', 'tomato']

# 1) 그냥 리스트 출력1
print(fruits)
# ['lemon', 'pear', 'watermelon', 'tomato']

# 2) 그냥 리스트 출력2
print(fruits[0], fruits[1], fruits[2], fruits[3])
# lemon pear watermelon tomato

# 3) for 반복문으로 순회하여 출력
for f in fruits:
    print(f, end=' ')
# lemon pear watermelon tomato

# 4) 아스테리스크(*) 사용하여 간편하게 출력
print(*fruit)
# lemon pear watermelon tomato
```

<br>

** 두개가 사용되는 경우는?

> ** 두개가 사용되는 경우는 키/값 페어를 언패킹하는데 사용됨

```python
date_info = {'year': '2020', 'month': '01', 'day': '7'}
new_info = {**date_info, 'day': '14'}
print(new_info)
# {'year': '2020', 'month': '01', 'day': '14'}
```



