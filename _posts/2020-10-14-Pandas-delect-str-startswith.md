---
layout: post
title: 특정 문자열로 시작하지 않는 행 추출
subtitle : 
tags: [Pandas]
author: JeongMin Lee
comments : True
---

## Pandas - 특정 문자열로 시작하지 않는 행 추출

특정 문자열로 시작하지 않는 행만 추출해보자

```python
import pandas as pd
df = pd.DataFrame(['[알림]오늘의 날씨','오늘의 뉴스','[알림]오늘의 음악','오늘의 영화'], columns=['today'])
df = df[~df['today'].str.startswith('[알림]')]
```

결과 : 

[알림]이라고 시작하는 컬럼을 제외한 나머지를 추출

![result1]({{ site.baseurl }}/assets/img/result1.PNG)

* endswith와 contains도 가능

```python
import pandas as pd
df = pd.DataFrame(['[알림]오늘의 날씨','오늘의 뉴스','[알림]오늘의 음악','오늘의 영화'], columns=['today'])
df = df[~df['today'].str.endswith('[알림]')]


import pandas as pd
df = pd.DataFrame(['[알림]오늘의 날씨','오늘의 뉴스','[알림]오늘의 음악','오늘의 영화'], columns=['today'])
df = df[~df['today'].str.contains('[알림]')]
```

