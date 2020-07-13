---
layout: post
title: 딕셔너리 다중 조건으로 정렬하기
subtitle : 
tags: [Python]
author: JeongMin Lee
comments : True
---

## 딕셔너리 키(key)와 값(value)을 기준으로 정렬하기 

​                     

dict.items()와 lambda함수를 사용하여 key와 value를 기준으로 정렬이 가능하다.

​           

* **ASC(오름차순) 정렬하기**

```python
# 코드
dictlist = {'a' : 2, 'g' : 5, 'i' : 4, 's' : 3, 'z' : 1}

# x[0] : 키(key)를 기준으로 정렬
sorted_dict = sorted(dictlist.items(), key=lambda x : x[0])
# x[1] : 값(value)을 기준으로 정렬
sorted_dict = sorted(dictlist.items(), key=lambda x : x[1])

# 결과
# [('a', 2), ('g', 5), ('i', 4), ('s', 3), ('z', 1)]
# [('z', 1), ('a', 2), ('s', 3), ('i', 4), ('g', 5)]
```

​             

* **DESC(내림차순) 정렬하기**
  * `reverse=True`를 사용하여 역순으로 정렬한다.

```python
# 코드
dictlist = {'a' : 2, 'g' : 5, 'i' : 4, 's' : 3, 'z' : 1}

# x[0] : 키(key)를 기준으로 정렬 
sorted_dict = sorted(dictlist.items(), reverse=True, key=lambda x : x[0])
# x[1] : 값(value)을 기준으로 정렬 
sorted_dict = sorted(dictlist.items(), reverse=True, key=lambda x : x[1])

# 결과
# [('z', 1), ('s', 3), ('i', 4), ('g', 5), ('a', 2)]
# [('g', 5), ('i', 4), ('s', 3), ('a', 2), ('z', 1)]
```





