---
layout: page
title: List - min max
description: >
  List
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.
### # N개의 양의 정수에서 가장 큰 수와 가장 작은 수의 차이를 출력하시오.
[입력]
첫 줄에 테스트 케이스의 수 T가 주어진다. ( 1 ≤ T ≤ 50 )
각 케이스의 첫 줄에 양수의 개수 N이 주어진다. ( 5 ≤ N ≤ 1000 )
다음 줄에 N개의 양수 ai가 주어진다. ( 1 ≤ ai≤ 1000000 )

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

~~~python
num = int(input())
res=num *[0]
ans=num*[0]
for i in range(num):    
    count = int(input())
    number=input().split()
    res[i] = list(map(int, number))
    ans[i]=max(res[i])-min(res[i])

for i in range(num):
    print("#{} {}".format(i+1,ans[i]))
~~~

~~~python
T = int(input())
for a in range(1,T+1):
    N = int(input())
    lis = list(map(int, input().split()))
    print("#{} {}".format(a,max(lis)-min(lis)))
~~~