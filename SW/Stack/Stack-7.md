---
layout: page
title: Stack - 토너먼트 카드게임
description: >
  Stack
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.
사다리 게임이 지겨워진 알고리즘 반 학생들이 새로운 게임을 만들었다. 가위바위보가 그려진 카드를 이용해 토너먼트로 한 명을 뽑는 것이다. 게임 룰은 다음과 같다.
1번부터 N번까지 N명의 학생이 N장의 카드를 나눠 갖는다. 전체를 두 개의 그룹으로 나누고, 그룹의 승자끼리 카드를 비교해서 이긴 사람이 최종 승자가 된다.
그룹의 승자는 그룹 내부를 다시 두 그룹으로 나눠 뽑는데, i번부터 j번까지 속한 그룹은 파이썬 연산으로 다음처럼 두개로 나눈다.
![stack7-1](../image/stack7-1.png)

두 그룹이 각각 1명이 되면 양 쪽의 카드를 비교해 승자를 가리고, 다시 더 큰 그룹의 승자를 뽑는 방식이다.
다음은 4명이 카드를 비교하는 경우로, 숫자 1은 가위, 2는 바위, 3은 보를 나타낸다. 만약 같은 카드인 경우 편의상 번호가 작은 쪽을 승자로 하고, 처음 선택한 카드는 바꾸지 않는다.
![stack7-2](../image/stack7-2.png)
N명이 학생들이 카드를 골랐을 때 1등을 찾는 프로그램을 만드시오.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤50
다음 줄부터 테스트 케이스의 별로 인원수 N과 다음 줄에 N명이 고른 카드가 번호순으로 주어진다. 4≤N≤100
카드의 숫자는 각각 1은 가위, 2는 바위, 3은 보를 나타낸다.

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 1등의 번호를 출력한다.

```python
def rcp(check, question): # 각대진의 승부를 기록하는 코드,가위바위보에서 진사람은 False로 만들어준다.
    if len(check) == 2:
        a,b = question[check[0]],question[check[1]]
        if a == b:
            question[check[1]] = False
        elif (a == 2 and b == 1) or (a==3 and b == 2) or (a==1 and b==3):
            question[check[1]] = False
        else:
            question[check[0]] = False
def solution(ind_stack,TM): # 전체 토너먼트 대진을 다 만들어주는 코드
    while True:
        a = TM[-1]
        mid = []
        for i in a:
            if (i[1] - i[0]) > 1:
                mid.append([i[0],(i[0]+i[1])//2])
                mid.append([(i[0]+i[1])//2+1,i[1]])
        TM.append(mid)
        if TM[-1] == []:
            TM.pop(-1)
            break
    return TM

def solution2(TM,question):#대진이 다 만들어진 후, 대진을 이용해 각 대진들의 승부를 보게하는 코드
    ans = 0
    while True:
        a = TM.pop(-1)
        for i in a:
            if i[0] != i[1]:
                check = []
                for b in range(i[0],i[1]+1):
                    if question[b] != False:
                        check.append(b)
                rcp(check,question)
        if len(TM) == 0:
            for i in range(0,len(question)):
                if question[i] != False:
                    ans = i
                    break
            break
    return ans       


T = int(input())
for t in range(1,T+1):
    N = int(input())
    question = list(map(int,input().split()))
    TM = [[[0,len(question)-1]]]
    ind_stack = list(map(int,list(range(0,len(question)))))
    solution(ind_stack,TM)
    print("#{} {}".format(t,1+solution2(TM, question)))
```
