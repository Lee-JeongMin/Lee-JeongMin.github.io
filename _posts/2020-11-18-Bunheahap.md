---
layout: post
title: 분해합_2231번(백준)
subtitle : 
tags: [Coding]
author: JeongMin Lee
comments : True

---

## 분해합(2231번)



##### 문제

------------------

어떤 자연수 N이 있을 때, 그 자연수 N의 분해합은 N과 N을 이루는 각 자리수의 합을 의미한다. 어떤 자연수 M의 분해합이 N인 경우, M을 N의 생성자라 한다. 예를 들어, 245의 분해합은 256(=245+2+4+5)이 된다. 따라서 245는 256의 생성자가 된다. 물론, 어떤 자연수의 경우에는 생성자가 없을 수도 있다. 반대로, 생성자가 여러 개인 자연수도 있을 수 있다.

자연수 N이 주어졌을 때, N의 가장 작은 생성자를 구해내는 프로그램을 작성하시오.

##### 입력

----------

첫째 줄에 자연수 N(1 ≤ N ≤ 1,000,000)이 주어진다.

##### 출력

-----------

첫째 줄에 답을 출력한다. 생성자가 없는 경우에는 0을 출력한다.



## 코드

생성자 M은 입력값인 N보다 항상 작으므로 for문의 범위를 1부터 N까지 완전탐색한다.

생성자 M의 각 자릿수의 값을 1의자리로 변환하는 과정을 재귀함수로 사용해서 구한다.

```python
# 메모리 : 29088KB, 시간 : 1092ms
def sum_num(i, hap):
    hap += i%10
    i = i // 10
    if i > 0:
        return sum_num(i, hap)
    else:
        return hap
    
def bunheahap(N):
    for i in range(1, N):
        hap = 0
        hap = sum_num(i, hap) + i
        if hap == N:
            return i
    else:
        return 0
    
N = int(input())
print(bunheahap(N))
```

하지만, 문제는 통과했지만 효율성을 개선할 필요가 있어 다른 사람코드를 확인해봤다.

```python
# 메모리 : 29088KB, 시간 : 72ms
N = int(input())

for i in range(max(1, N-54), N+1):
    if N == i + sum(list(map(int, str(i)))):
        print(i)
        exit(0)
print(0)
```

코드 작성자는 생성자의 범위를 N-54보다 크거나 같고 N보다 작거나 같다로 두어 반복의 수를 줄였다. 이유는 [https://itadventure.tistory.com/158](https://itadventure.tistory.com/158)를 참고하면 좋을꺼같다.

또한, 나는 재귀함수를 사용해 분해합을 구했지만 본 코드 작성자는 `i + sum(list(map(int, str(i))))`을 사용해 합을 구한다.

∴  효율성을 향상시킬 수 있다.



##### 알고리즘 분류

------

* 브루트포스 알고리즘