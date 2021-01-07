---
layout: post
title: 파이썬 알고리즘 인터뷰_파이썬 문법
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_파이썬 문법

------



* [파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리



##### 인텐트(Intent)

------

파이썬의 대표적인 특징인 인텐트(Intent)는 공식 가이드인 PEP 8에 따라 공백 4칸을 원칙으로 한다.

추가로, 아래의 코드와 주석과 같은 기준들이 포함되어있다.

```python
# 첫 번째 줄에 파라미터가 있다면, 파이미터가 시작되는 부분에 맞춘다.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 첫 번째 줄에 파라미터가 없다면, 공백 4칸(인텐트)를 추가하여 다른 행과 구분한다.
def long_function_name(
		var_one, var_two, var_three,
		var_four):
    print(var_one)
    
# 여러 줄로 나눠쓸 경우 다음 행과 구분되도록 인텐트를 추가한다.
foo = long_function_name(
	var_one, var_two,
	var_three, var_four)
```



##### 네이밍 컨벤션(Naming Convention)

------

파이썬의 변수명은 각 단어를 밑줄(_)로 구분하여 표기하는 스네이크 케이스(Snake Case)를 따른다.



##### 타입 힌트(Type Hint)

------

파이썬에서도 타입 힌트(Type Hine)를 사용해 변수에 타입을 지정할 수 있다.

코드를 통해 타입 힌트를 사용할 때와 사용하지 않을때를 비교해본다.

* Type Hint를 사용하지 않은 경우

```python
def fn(a):
    ...
```

빠르게 정의해서 사용할 수 있는 것이 장점이지만, 파라미터 a에 정수를 넣어야하는지 문자를 넣어야하는지 알 수가 없다. 프로젝트의 규모가 커지면서 가독성을 떨어트려 버그 유발에 주범이 된다.

* Type Hint를 사용한 경우

```python
def fn(a: int) -> bool:
    ...
```

타입 힌트를 사용하면 파라미터 a에는 정수를 넣어햐함을 확실히 알 수 있으며, 리턴값으로 True or False를 리턴할 것이라는 점도 알 수 있다. 

타입 힌트에 오류를 파악하고 싶다면 `mypy`를 사용하면 된다.

```bash
$ pip install mypy # mypy 설치
$ mypy solution.py # mypy 사용
```



##### 리스트 컴프리헨션(List Comprehension)

------

리스트 컴프리헨션이란?

	- 기존 리스트를 기반으로 새로운 리스트를 만들어내는 구문이다.

다방면에 유용하게 사용되며 람다(lambda)에 map, filter를 사용하는 것보다 가독성이 뛰어나다.

아래의 예시 코드는 홀수 인 경우 2를 곱해 출력하는 코드이다.

```python
# List Comprehension을 사용한 경우
[n*2 for n in range(1, 10+1) if n % 2 == 1 ]

# List Comprehension을 사용하지 않은 경우
a = []
for n in range(1, 10+1):
    if n % 2 == 1:
        a.append(n*2)
```

버전 2.7 이후에는 딕셔너리도 가능하다.

```python
# Dictionary Comprehension을 사용한 경우
a = {key: value for key, value in original.items()}

# Dictionary Comprehension을 사용하지 않은 경우
a = {}
for key, value in original.items():
    a[key] = value
```



##### 제너레이터(Generator)

------

제너레이터란?

* 루프의 반복 동작을 제어할 수 있는 루틴 형태를 의미한다.

예를 들어, 임의의 조건으로 숫자 1억개를 만들어내 계산하는 프로그램인 경우, 제너레이터가 없다면 메모리 어딘가에 만들어낸 숫자 1억개를 보관하고 있어야한다. 하지만 제너레이터를 사용하면 필요할 때 언제든 숫자를 만들어낼 수 있다.

`yield`구문을 사용하면 제너레이터를 리턴할 수 있다. `yield`는 제너레이터가 여기까지 실행 중이던 값을 내보낸다는 의미로, 리턴한 다음 함수는 종료되지 않고 계속해서 맨 끝에 도달할 때까지 실행된다. 

```python
def get_natural_number():
    n = 0
    while True:
        n += 1
        yield n
        
# 함수의 리턴값은 제너레이터가 된다.
>>> get_natural_number()
<generator object get_natural_number at 0x00000163602E09C8>
```

만약 다음 값을 생성하려면 next()로 추출하면 된다. ex) 100개의 값을 생성하고 싶다면 아래의 코드처럼 사용하면 된다.

```python
g = get_natural_number()
for _ in range(0, 100):
    print(next(g))
```

또한, 제너레이터는 여러 타입의 값을 하나의 함수에서 생성하는 것도 가능하다.

```python
def generator():
    yield 1
    yield 'String'
    yield True
    
g = generator()
g_value = next(g)
print('값 : {}, 타입 : {}'.format(g_value,type(g_value)))
# 값 : 1, 타입 : <class 'int'>
g_value = next(g)
print('값 : {}, 타입 : {}'.format(g_value,type(g_value)))
# 값 : String, 타입 : <class 'str'>
g_value = next(g)
print('값 : {}, 타입 : {}'.format(g_value,type(g_value)))
# 값 : True, 타입 : <class 'bool'>
```



##### range

------

제너레이터의 방식을 활용하는 대표적인 함수는 range()이다.

아래의 코드와 같이 사용된다.

```python
list(range(5))
# [0, 1, 2, 3, 4]

range(5)
# range(0, 5)

type(range(5))
# <class 'range'>

for i in range(5):
    print(i, end='')
# 0 1 2 3 4
```

range()는 range 클래스를 리턴하며, for 문에서 사용할 경우 내부적으로는 제너레이터의 next()를 호출하듯 매번 다음 숫자를 생성해낸다.

다음은 숫자 100만개를 생성하는 2가지 방법이다.

```python
a = [n for n in range(1000000)]
b = range(1000000)
```

둘의 길이를 비교해보면 동일하게 100만개가 출력된다.

하지만 a에는 이미 생성된 값이 담겨 있고, b는 생성해야 한다는 조건만 존재한다.

a와 b의 메모리 점유율을 비교해보자

```python
sys.getsizeof(a)
# 8697464

sys.getsizeof(b)
#48
```

b는 생성 조건만 보관하고 있기 때문에 a에 비해 메모리 점유율이 현저히 적다. 또한, b는 인덱스 접근이 바로 가능해 리스트와같이 사용할 수 있다.



##### enumerate

------

enumerate란?

* 순서가 있는 자료형(list, set, tuple 등)을 인덱스를 포함한 enumerate객체로 리턴한다.

```python
a = [1, 2, 3, 2, 45, 2, 5]
enumerate(a)
# <enumerate at 0x16363b81818>
list(enumerate(a))
# [(0, 1), (1, 2), (2, 3), (3, 2), (4, 45), (5, 2), (6, 5)]
```

a = ['a1', 'b1', 'c1']의 경우에는 어떻게 리스트의 인덱스와 값을 한번에 출력할까?

```python
a = ['a1', 'b1', 'c1']
for idx, val in enumerate(a):
    print(idx, val)
```



##### // 나눗셈 연산자

------

// 연산자란?

* 몫을 구하는 연산자이다.

% 연산자란?

* 나머지를 구하는 연산자이다.

```python
5/3
# 1.6666666666666667

5//3
# 1

5%3
# 2
```

몫과 나머지를 동시에 구하려면 어떻게 해야할까?

divmod()함수를 사용하면 된다.

```python
divmod(5, 3)
# (1, 2)
```



##### print

------

가장 쉽게 값을 출력하는 방법은 콤마(,)로 구분하는 것이다. 띄어쓰기를 사용해 값을 구분해준다.

```python
print('A1', 'B2')
# A1 B2
```

sep 파라미터를 사용해 구분자를 다른 문자,기호로 바꿀 수 있다.

```python
print('A1', 'B2', sep='/')
# A1/B2
```

print()는 항상 줄바꿈을 하기 때문에 긴 루프의 값을 반복적으로 출력하면 디버깅이 어렵다. 이때, end 파라미터를 사용해 줄바꿈을 하지 않도록 제한할 수 있다.

```python
print('aa', end=' ')
print('bb')
# aa bb
```

리스트를 출력할 때는 join()으로 묶어서 처리한다.

```python
a = ['A', 'B']
print(' '.join(a))
# A B
```

format을 사용해 원하는 데이터를 위치에 맞게 출력할 수 있다.

```python
idx = 1
fruit = 'Apple'

print('{0} : {1}'.format(idx+1, fruit)) # 인덱스를 부여해 사용 가능하다.
# 2 : Apple

print('{1} : {0}'.format(idx+1, fruit)) # 인덱스의 순서를 변환해 사용 가능하다.
# Apple : 2

print('{} : {}'.format(idx+1, fruit)) # 인덱스를 생략할 수 있다. 
# 2 : Apple
```

f-string방법을 사용해 출력이 가능하다. `.format`을 부여하는 방식에 비해 훨씬 간결하고 직관적이며 속도도 빠르다. (파이썬 3.6+에서만 지원)

```python
print(f'{idx+1}: {fruit}')
# 2: Apple
```



##### pass

------

pass의 기능은?

* 널 연산으로 아무것도 하지 않는 기능이다.

pass를 사용해 목업 인터페이스를 구현할 때 편리하다.



##### locals

------

locals()란?

* 로컬 심볼 테이블 딕셔너리를 가져오는 메소드이다.

로컬에 선언된 모든 변수를 조회할 수 있는 강력한 명령이므로 디버깅에 많은 도움이 된다. 

클래스의 특정 메소드 내부에서나 함수 내부의 로컬 정보를 조회해 잘못 선언한 부분이 없는지 확인하는 용도로 활용이 가능하다.

```python
import pprint
pprint.pprint(locals())

# {'nums': [2, 7, 11, 15],
#  'pprint': <module 'pprint' from '/usr/lib/python3.8/pprint.py'>,
#  'self': <__main__.Solution object at 0x7f0994769d90>,
#   'target': 9}
# 클래스 메소드 내부의 모든 로컬 변수를 출력해 주기 때문에 디버깅에 많은 도움이 된다.
```



