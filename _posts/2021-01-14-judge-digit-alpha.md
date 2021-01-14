---
layout: post
title: 문자열 판별하기(isdigit/isalpha/isalnum)
subtitle : 
tags: [Python]
author: JeongMin Lee
comments : True
---

## 문자열 판별하기(isdigit/isalpha/isalnum)



### isdigit

> 문자열이 숫자인지 아닌지를 True, False로 반환한다.

```python
str1 = '123'
str2 = '010-1234-1234'
str3 = '1 2 3 4'
str4 = 'A9'

print(str1.isdigit())
print(str2.isdigit())
print(str3.isdigit())
print(str4.isdigit())
```

 Result

```python
 # 완전히 숫자로만 이루어진 경우
True
 # 숫자외의 문자, 특수문자와 함께 사용된 경우
False 
False
False
```

<br><br>

### isalpha

> 문자열이 문자인지 아닌지를 True, False로 반환한다. (영어, 한글 지원)

```python
str1 = 'hello'
str2 = '안녕하세요'
str3 = 'hello python'
str4 = 'h2h2'

print(str1.isalpha())
print(str2.isalpha())
print(str3.isalpha())
print(str4.isalpha())
```

Result

```python
# 완전히 문자로만 이루어진 경우(영어, 한글 가능)
True
True
# 문자 외의 특수문자와 숫자가 함께 있는 경우
False
False
```

<br><br>

### isalnum

> 문자열이 문자 또는 숫자인지  아닌지를  True, False로 반환한다.

```python
str1 = 'ㄱㄴㄷ3'
str2 = 'python1'
str3 = '01012341234'
str4 = 'hello python2'
str5 = 'a,b,c'

print(str1.isalnum())
print(str2.isalnum())
print(str3.isalnum())
print(str4.isalnum())
print(str5.isalnum())
```

Result

```python
# 완전히 문자 또는 숫자로 이루어진 경우(영어, 한글 가능)
True
True
True
# 공백 또는 특수문자가 포함되어있는 경우
False
False
```

