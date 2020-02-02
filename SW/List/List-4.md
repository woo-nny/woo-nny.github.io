---
layout: page
title: List - 구간 합
description: >
  List
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.
N개의 정수가 들어있는 배열에서 이웃한 M개의 합을 계산하는 것은 디지털 필터링의 기초연산이다.
M개의 합이 가장 큰 경우와 가장 작은 경우의 차이를 출력하는 프로그램을 작성하시오.
다음은 N=5, M=3이고 5개의 숫자 1 2 3 4 5가 배열 v에 들어있는 경우이다.
![list4](../image/2.png)
답은 12와 6의 차인 6을 출력한다.


[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  ( 1 ≤ T ≤ 50 )
다음 줄부터 테스트케이스의 첫 줄에 정수의 개수 N과 구간의 개수 M 주어진다. ( 10 ≤ N ≤ 100,  2 ≤ M ＜ N )
다음 줄에 N개의 정수 ai가 주어진다. ( 1 ≤ a ≤ 10000 )

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

~~~python
T = int(input())
for i in range(T):
    N, M = map(int,input().split())
    num = list(map(int,input().split()))
    res=[] #구간 합 전체 공간
    for j in range(N-M+1):
        res.append(sum(num[j:j+M])) #구간 합 전체 공간을 슬라이스로 합친다음 res에 추가
    print("#{} {}".format(i+1,max(res)-min(res)))
~~~

~~~python
from sys import stdin
T = int(stdin.readline())
for a in range(1,T+1):
    N, M = map(int, stdin.readline().split())
    lis = list(map(int, stdin.readline().split()))
    sumlis = [0,sum(lis[0:M])] # 최대값과 최소값을 넣을 공간
    for b in range(0,N-M+1): #M개씩 넣어서 나올 모든 숫자를 비교한다.
        c = sum(lis[b:b+M])
        if c > sumlis[0]:
            sumlis[0] = c
        elif c < sumlis[1]:
            sumlis[1] = c
    print("#{} {}".format(a,sumlis[0]-sumlis[1]))
~~~