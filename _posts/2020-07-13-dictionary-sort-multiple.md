---
layout: post
title: 딕셔너리 다중 조건으로 정렬하기
subtitle : 
tags: [Python]
author: JeongMin Lee
comments : True
---



## 딕셔너리 다중 조건으로 정렬하기

​                

sorted와 lambda함수를 사용하여 dictionary를 여러 키로 정렬이 가능하다.

​        

```python
# 코드
dictlist = [
    {'height' : 170, 'weight' : 60, 'name' : '홍길동'},
    {'height' : 160, 'weight' : 90, 'name' : '이몽룡'},
    {'height' : 165, 'weight' : 55, 'name' : '성춘향'},
    {'height' : 180, 'weight' : 70, 'name' : '대조영'},
    {'height' : 180, 'weight' : 85, 'name' : '김개똥'},
    {'height' : 165, 'weight' : 65, 'name' : '아무개'}
]

# height 높은 순, weight 낮은 순
sorted_dict = sorted(dictlist, key = lambda x : (-x['height'], x['weight']))

# 결과
#[{'height': 180, 'weight': 70, 'name': '대조영'},
# {'height': 180, 'weight': 85, 'name': '김개똥'},
# {'height': 170, 'weight': 60, 'name': '홍길동'},
# {'height': 165, 'weight': 55, 'name': '성춘향'},
# {'height': 165, 'weight': 65, 'name': '아무개'},
# {'height': 160, 'weight': 90, 'name': '이몽룡'}]
```

​        

`lambda`함수를 사용하여 다중 조건을 설정할 수 있다. 

첫번째 키인 `height`를 기준으로 내림차순으로 정렬한 후, 값이 같은 경우 두번째 키인 `weight`를 기준으로 오름차순으로 정렬한다.

이때, column 앞에 `-`를 붙이면 내림차순(5, 4, 3, 2, 1), 아무것도 안붙이면 오름차순(1, 2, 3, 4, 5)으로 정렬된다.