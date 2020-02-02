---
layout: page
title: List - 특별한 정렬
description: >
  List
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

보통의 정렬은 오름차순이나 내림차순으로 이루어지지만, 이번에는 특별한 정렬을 하려고 한다.
N개의 정수가 주어지면 가장 큰 수, 가장 작은 수, 2번째 큰 수, 2번째 작은 수 식으로 큰 수와 작은 수를 번갈아 정렬하는 방법이다.
예를 들어 1부터 10까지 10개의 숫자가 주어지면 다음과 같이 정렬한다.
10 1 9 2 8 3 7 4 6 5
주어진 숫자에 대해 특별한 정렬을 한 결과를 10개까지 출력하시오

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1<=T<=50
다음 줄에 정수의 개수 N이 주어지고 다음 줄에 N개의 정수 ai가 주어진다. 10<=N<=100, 1<=ai<=100

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 특별히 정렬된 숫자를 10개까지 출력한다.

```python
test = int(input())

for n in range(test):
    NUM = int(input())
    a = map(int, input().split())
    a=list(a)
    res =[]
    for N in range(10): #res의 들어갈 인댁스번호를 설정한다.
        if N%2==0: # 큰 숫자가 들어가야할 자리
            res.append(max(a)) #a에 들어있는 리스트중 가장 큰 수를 res에 넣고
            a.pop(a.index(max(a))) # pop해준다.
        else: #작은 숫자가 들어가야할 자리
            res.append(min(a))# 위와반대
            a.pop(a.index(min(a)))
    print("#{}".format(n+1), end=' ')
    for i in range(10):
        print(res[i], end=" ")#결과 도출
    print()
```

```python
T = int(input())
for t in range(1,T+1):
    N = int(input())
    ai = sorted(list(map(int, input().split())))#한번에 정렬된 상태로 들어오게함
    ans = ""
    for a in range(0,10):
        if a % 2 == 0:#a가 짝수이면
            ans +=" "+str(ai.pop(-1)) #가장 큰 수를 pop하고 ans에 추가
        else: #위와 반대
            ans += " "+str(ai.pop(0))
    print("#{}{}".format(t,ans))
```