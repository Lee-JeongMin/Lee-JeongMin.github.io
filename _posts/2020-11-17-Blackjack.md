---
layout: post
title: 블랙잭_2798번(백준)
subtitle : 
tags: [Coding]
author: JeongMin Lee
comments : True
---

## 블랙잭(2798번)



##### 문제

------------------

카지노에서 제일 인기 있는 게임 블랙잭의 규칙은 상당히 쉽다. 카드의 합이 21을 넘지 않는 한도 내에서, 카드의 합을 최대한 크게 만드는 게임이다. 블랙잭은 카지노마다 다양한 규정이 있다.

한국 최고의 블랙잭 고수 김정인은 새로운 블랙잭 규칙을 만들어 상근, 창영이와 게임하려고 한다.

김정인 버전의 블랙잭에서 각 카드에는 양의 정수가 쓰여 있다. 그 다음, 딜러는 N장의 카드를 모두 숫자가 보이도록 바닥에 놓는다. 그런 후에 딜러는 숫자 M을 크게 외친다.

이제 플레이어는 제한된 시간 안에 N장의 카드 중에서 3장의 카드를 골라야 한다. 블랙잭 변형 게임이기 때문에, 플레이어가 고른 카드의 합은 M을 넘지 않으면서 M과 최대한 가깝게 만들어야 한다.

N장의 카드에 써져 있는 숫자가 주어졌을 때, M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 구해 출력하시오.

##### 입력

----------

첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다. 둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는다.

합이 M을 넘지 않는 카드 3장을 찾을 수 있는 경우만 입력으로 주어진다.

##### 출력

-----------

첫째 줄에 M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 출력한다.



## 코드

① 3개의 조합을 찾아 합을 구한다.

② 합이 M보다 크지 않으며 and M과 합의 차이가 더 작은 값이 blackjack이 된다.

```python
# 메모리 : 29088KB, 시간 : 96ms
def blackjack_cardgame(N, M, num_ls):
    blackjack = 0
    for i in range(N-2):
        for j in range(i+1, N-1):
            for k in range(j+1, N):
                score = num_ls[i]+num_ls[j]+num_ls[k]  
                if score <= M and M - score < M - blackjack:
                    blackjack = score
    return blackjack

N, M = map(int, input().split())
num_ls = list(map(int, input().split()))
print(blackjack_cardgame(N, M, num_ls))
```

python의 itertools 라이브러리를 사용해 조합을 구할 수 있다.

다만, 효율성이 떨어진다.

```python
# 메모리 : 40736KB, 시간 : 148ms
from itertools import combinations

def blackjack_cardgame(N, M, num_ls):
    blackjack = 0
    num_combi = list(combinations(num_ls, 3))
    for i in num_combi:
        score = sum(list(i)) 
        if score <= M and M - score < M - blackjack:
            blackjack = score
    return blackjack

N, M = map(int, input().split())
num_ls = list(map(int, input().split()))
print(blackjack_cardgame(N, M, num_ls))
```

