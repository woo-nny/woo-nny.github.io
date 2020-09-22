---
layout: page
title: Stack - 미로
description: >
  Stack
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

NxN 크기의 미로에서 출발지에서 목적지에 도착하는 경로가 존재하는지 확인하는 프로그램을 작성하시오. 도착할 수 있으면 1, 아니면 0을 출력한다.
주어진 미로 밖으로는 나갈 수 없다.
다음은 5x5 미로의 예이다.

13101

10101

10101

10101

10021

마지막 줄의 2에서 출발해서 0인 통로를 따라 이동하면 맨 윗줄의 3에 도착할 수 있는지 확인하면 된다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1<=T<=50
다음 줄부터 테스트 케이스의 별로 미로의 크기 N과 N개의 줄에 걸쳐 미로의 통로와 벽에 대한 정보가 주어진다. 0은 통로, 1은 벽, 2는 출발, 3은 도착이다. 5<=N<=100

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 계산결과를 정수로 출력하거나 또는 ‘error’를 출력한다.

```python
def dfs(lis,stack):
    while True:
        a, b = stack.pop(-1)
        addlis = [[a+1,b],[a-1,b],[a,b+1],[a,b-1]] # 상하 좌우
        for i in addlis:
            if 0 <= i[0] < len(lis) and 0<= i[1] < len(lis): # 전체 미로 크기 벗어나는 경우 배제
                if lis[i[0]][i[1]] == 0:
                    lis[i[0]][i[1]] = 4 # 4는 지나간 흔적
                    stack.append(i)
                elif lis[i[0]][i[1]] == 3:
                    return 1
        if len(stack) == 0:
            break
    return 0

T = int(input())
for t in range(1,T+1):
    N = int(input())
    lis = []
    for a in range(N):
        lis.append(list(map(int, input().strip())))
    stack = []
    for j in range(0,len(lis)):
        for k in range(0,len(lis)):
            if lis[j][k] == 2:
                stack.append([j,k])
    print("#{} {}".format(t,dfs(lis,stack)))
```