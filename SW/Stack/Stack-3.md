---
layout: page
title: Stack - 그래프 경로
description: >
  Stack
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

V개 이내의 노드를 E개의 간선으로 연결한 방향성 그래프에 대한 정보가 주어질 때, 특정한 두 개의 노드에 경로가 존재하는지 확인하는 프로그램을 만드시오.
두 개의 노드에 대해 경로가 있으면 1, 없으면 0을 출력한다.
예를 들어 다음과 같은 그래프에서 1에서 6으로 가는 경로를 찾는 경우, 경로가 존재하므로 1을 출력한다.
![stack3](../image/stack3.png)
노드번호는 1번부터 존재하며, V개의 노드 중에는 간선으로 연결되지 않은 경우도 있을 수 있다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤50
다음 줄부터 테스트 케이스의 첫 줄에 V와 E가 주어진다. 5≤V≤50, 4≤E≤1000
테스트케이스의 둘째 줄부터 E개의 줄에 걸쳐, 출발 도착 노드로 간선 정보가 주어진다.
E개의 줄 이후에는 경로의 존재를 확인할 출발 노드 S와 도착노드 G가 주어진다.

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
T = int(input())
for t in range(1,T+1):
    V, E = list(map(int, input().split())) # 최종 번호, 경로 갯수
    checklist = []
    for e in range(0,E):
        checklist.append(list(map(int, input().split()))) # 경로 입력
    start, end = list(map(int, input().split())) #시작 끝 입력
    ans = 0
    anslis = []
    for a in checklist: # 최초 시작할 노드 정해줌.
        if a[0] == start:
            anslis.append(a[1])
    check = True
    while check:
        mid = []
        for a in checklist:#스택의 top위치의 원소를 이용해 자식이 있는지 없는지 판단
            if a[0] == anslis[-1]:
                mid.append(a[1])#자식이 있다면 중간값에 추가해주고
        if end in mid:#중간값에 찾는 값이 있다면, 최종적으로 목표에 도달 할 수있으므로 종료
            ans = 1
            break
        anslis.pop(-1)#그렇지 않다면 pop을하고
        anslis += mid#push를 해준다
        if len(anslis) == 0:
            ans = 0
            break
    print("#{} {}".format(t,ans))
```
