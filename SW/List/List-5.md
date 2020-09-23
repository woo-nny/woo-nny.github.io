---
layout: page
title: List - NLP
description: >
  List
hide_description: true
comments: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

그림과 같이 인덱스가 있는 10x10 격자에 빨간색과 파란색을 칠하려고 한다.
N개의 영역에 대해 왼쪽 위와 오른쪽 아래 모서리 인덱스, 칠할 색상이 주어질 때, 칠이 끝난 후 색이 겹쳐 보라색이 된 칸 수를 구하는 프로그램을 만드시오.
주어진 정보에서 같은 색인 영역은 겹치지 않는다.
![list5](../image/3.jpg)
예를 들어 2개의 색칠 영역을 갖는 위 그림에 대한 색칠 정보이다.

2
2 2 4 4 1  ( [2,2] 부터 [4,4] 까지 color 1 (빨강) 으로 칠한다 )
3 3 6 6 2 ( [3,3] 부터 [6,6] 까지 color 2 (파랑) 으로 칠한다 )

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.   ( 1 ≤ T ≤ 50 )
다음 줄부터 테스트케이스의 첫 줄에 칠할 영역의 개수 N이 주어진다. ( 2 ≤ N ≤ 30 )
다음 줄에 왼쪽 위 모서리 인덱스 r1, c1, 오른쪽 아래 모서리 r2, c2와 색상 정보 color가 주어진다. ( 0 ≤ r1, c1, r2, c2 ≤ 9 )
color = 1 (빨강), color = 2 (파랑)

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
test = int(input())

for n in range(test):
    N = int(input())
    red_sqr = []
    blue_sqr = []
    for N in range(N):
        r1, c1, r2, c2, color = map(int,input().split())#row,column의 시작과 끝을 점으로 받고, 색을 넣는다.
        for y in range(c1,c2+1):
            for x  in range(r1,r2+1): 
                if color ==1:# 빨간색이면 red_sqr에 넣어줘 빨간색 면을 만든다
                    red_sqr.append((y,x))
                elif color==2:# 파란색이면 blue_sqr에 넣어줘 파란색 면을 만든다
                    blue_sqr.append((y,x))
    res = []
    if len(red_sqr) > len(blue_sqr): # 크기 비교
        for i in blue_sqr: # 레드가 크면 파란색을 다 돌려서 
            if i in red_sqr: # 만약 파란색영역에 빨간색이 있으면
                res.append(i) # 결과값에 추가한다
    if len(red_sqr) < len(blue_sqr): #위와 반대의 상황
        for i in red_sqr:
            if i in blue_sqr:
                res.append(i)

    print('#%s %d'%(n, len(res)))

```

```python
T = int(input())
for test in range(1,T+1):
    N = int(input())
    graph = []
    for a in range(0,10): #최대 영역이 10이라 했으므로, 10의 제한을 줌
        graph.append([])
        for b in range(0,10):
            graph[a].append(0)
    for num in range(0,N):
        a = list(map(int, input().split()))
        if a[-1] == 1: # 끝에 색깔이 들어오므로 색을 판별한다.
            for b in range(a[0],a[2]+1): # 빨간색의 영역을 전부다 1을 더 해준다.=
                for c in range(a[1],a[3]+1):
                    graph[b][c] += 1
        else:
            for b in range(a[0],a[2]+1): # 파란색인 경우로 해준다
                for c in range(a[1],a[3]+1):
                    graph[b][c] += 100 # 파란색 영역이면 100을 더 해준다.
    cnt = 0
    for a in graph:# 전체 영역중에서 합이 101이상인 것을 찾아내어 갯수를 샌다.
        for b in a:
            if b >100:
                cnt += 1
    print("#{} {}".format(test,cnt))

```
