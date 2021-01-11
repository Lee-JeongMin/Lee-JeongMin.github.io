---
layout: post
title: 파이썬 알고리즘 인터뷰_문자열 조작
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_문자열 조작

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 유효한 팰린드롬](#문제01-유효한-팰린드롬 )
* 문제02
* 문제03 
* 문제04
* 문제05
* 문제06

<br/>

##### 문제01 유효한 팰린드롬 

-----

> [https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)
>
> 주어진 문자열이 팰린드롬인지 확인해라. 대소문자를 구분하지 않으며, 영문자와 숫자만을 대상으로 한다.
>
> **Example 1:**
>
> ```python
> Input: "A man, a plan, a canal: Panama"
> Output: true
> ```
>
> **Example 2:**
>
> ```python
> Input: "race a car"
> Output: false
> ```

* 내 코드

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # lower()함수로 소문자로 변경 후, 정규표현식을 사용해 영어와 숫자만 대상으로 한다.
        text = list(re.sub('[^a-z0-9]','',s.lower()))
        
		# 맨 앞의 문자와 맨 뒤의 문자를 추출해 비교한다.
        while len(text) > 1:
            if text.pop() != text.pop(0):
                return False

        return True
    
isPalindrome("A man, a plan, a canal: Panama")
```

Result

>  Runtime : 232ms, Memory : 15.9MB

<br>

* 풀이1_리스트로 변환

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # isalnum()을 사용해 영문자와 숫자를 판별후 소문자로 변환한다.
        strs = []
        for char in s:
            if char.isalnum():
                strs.append(char.lower())
		# 맨 앞의 문자와 맨 뒤의 문자를 추출해 비교한다.
        while len(strs) > 1:
            if strs.pop() != strs.pop(0):
                return False

        return True
isPalindrome("A man, a plan, a canal: Panama")
```

- isalnum() : 문자열이 영어, 한글 혹은 숫자로 되어있으면 참 리턴, 아니면 거짓 리턴

Result

>  Runtime : 292ms, Memory : 20.1MB

<br>

* 풀이2_데크 자료형을 이용한 최적화

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # 자료형 데크로 선언
        strs : Deque = collections.deque()
        # isalnum()을 사용해 영문자와 숫자를 판별후 소문자로 변환한다.
        for char in s:
            if char.isalnum():
                strs.append(char.lower())
       # 맨 앞의 문자와 맨 뒤의 문자를 추출해 비교한다.
        while len(strs) > 1:
            if strs.popleft() != strs.pop():
                return False
        return True
    
isPalindrome("A man, a plan, a canal: Panama")
```

Result

>  Runtime : 68ms, Memory : 19.4MB

<br>

`+데크 설명 추가하기`

<br>

* 풀이3_슬라이싱 사용

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # 소문자 변환
        s = s.lower()
        # 정규식으로 불필요한 문자 필터링
        s = re.sub('[^a-z0-9]', '', s)
        
        # 슬라이싱
        return s == s[::-1]
    
isPalindrome("A man, a plan, a canal: Panama")
```

Result

>  Runtime : 36ms, Memory : 15.6MB

<br>

**문자열 슬라이싱**

![example]({{ site.baseurl }}/assets/img/example.jpg){:.width-30 .align="left"}
*↑슬라이싱에 사용할 예시 문장 및 인덱스*

| 슬라이싱 방법 | 결과       | 설명                                                         |
| ------------- | ---------- | ------------------------------------------------------------ |
| s[1:4]        | 녕하세     | 인덱스 1에서 4이전까지 표현                                  |
| s[1:-2]       | 녕하       | 인덱스 1에서 -2이전까지 표현                                 |
| s[1:]         | 녕하세요   | 문자열 시작 또는 끝은 생략 가능                              |
| s[:]          | 안녕하세요 | 둘다 생략하면 사본을 리턴한다.                               |
| s[1:100]      | 녕하세요   | 인덱스가 지나치게 클 경우 문자열의 최대 길이만큼만 표현, S[1:]와 동일하다. |
| s[-1]         | 요         | 마지막 문자(뒤에서 첫 번째)                                  |
| s[-4]         | 녕         | 뒤에서 4번째                                                 |
| s[:-3]        | 안녕       | 뒤에서 3번째 문자 앞까지                                     |
| s[-3:]        | 하세요     | 뒤에서 3번째 문자부터 끝까지                                 |
| s[::1]        | 안녕하세요 | 1은 기본값으로 동일하다.                                     |
| s[::-1]       | 요세하녕안 | 문자열을 뒤집는다.                                           |
| s[::2]        | 안하요     | 2칸씩 앞으로 이동한다.                                       |
| s[::-3]       | 요녕       | 뒤에서부터 3칸씩 이동한다.                                   |

