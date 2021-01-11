---
layout: post
title: 파이썬 알고리즘 인터뷰_빅오(big-O)
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
html header: <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
---

### 파이썬 알고리즘 인터뷰_빅오(big-O)

------



* [파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리

<br/>

##### 빅오(O, big-O)

------

>  점근적 실행 시간을 표기할 때 가장 널리쓰이는 수학적 표기법 중 하나이다.

<br/>

점근적 실행 시간은 시간 복잡도를 의미한다.

<br/>

##### 시간 복잡도

-------

> 어떤 알고리즘을 수행하는 데 걸리는 시간을 설명하는 계산 복잡도를 의미한다.

* 빅오로 시간 복잡도를 표기할 때는 최고차항만 표기하고 상수항은 무시한다.

  ex)  \\({4n}^{2}+3n+4\\) 의 시간복잡도는 \\({4n}^{2}\\) 만 고려해 \\(O\({n}^{2})\\)이다.

  <br/>

##### 빅오 표기법 & 종류

------

![big_O]({{ site.baseurl }}/assets/img/big_O.jpg)

![bigO_n]({{ site.baseurl }}/assets/img/bigO_n.png){: .width-60}


* O(1)
  
  * 상수시간(Constant Time)
  * 입력값이 아무리 커도 실행시간은 일정
* 예제 : 해시 테이블의 조회 및 삽입
  
* O(log n)

  * 로그시간 또는 대수시간(Logarithmic)
  * 실행 시간은 입력값에 영향을 받지만 로그는 매우 큰 입력값에도 크게 영향을 받지 않음
  * 예제 : 이진 검색

* O(n)

  * 선형시간(Linear Time)
  * 입력값만큼 실행 시간에 영향을 받으며, 입력값과 시간이 정비례하게 증감
  * 예제 : 정렬되지 않은 리스트에서 최댓값 또는 최솟값을 찾는 경우(모든  입력값을 한 번 이상 살핌)

* O(nlogn)

  * 로그선형시간(Log-Linear)
  * 예제 : 병합 정렬을 비롯한 대부분의 효율 좋은 정렬 알고리즘

* O(n^2)

  * 제곱시간(Quadratic)
  * 예제 : 버블 정렬 같은 비효율적인 정렬 알고리즘 해당

* O(2^n)

  * 지수시간(Exponential)
  * 예제 : 피보나치 수를 재귀로 계산하는 알고리즘이 해당

* O(n!)

  * 가장 느린 알고리즘으로 입력값이 조금만 커져도 웬만한 다항 시간 내에는 계산이 어려움

  * 예제 : 각 도시를 방문하고 돌아오는 가장 짧은 경로를 찾는 외판원 문제를 부르트 포스로 풀이할 때 해당

    