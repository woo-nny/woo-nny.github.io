---
layout: page
title: String - 회문
description: >
  String
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

ABBA처럼 어느 방향에서 읽어도 같은 문자열을 회문이라 한다. NxN 크기의 글자판에서 길이가 M인 회문을 찾아 출력하는 프로그램을 만드시오.
회문은 1개가 존재하는데, 가로 뿐만 아니라 세로로 찾아질 수도 있다.
예를 들어 N=10, M=10 일 때, 다음과 같이 회문을 찾을 수 있다.
![string2](../image/string2.png)

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤50
다음 줄부터 테스트케이스의 첫 줄에 N과 M이 주어진다. 10≤N≤100, 5≤M≤N
다음 줄부터 N개의 글자를 가진 N개의 줄이 주어진다.

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
TEST = int(input())
for T in range(1,TEST+1):
    N, M = list(map(int, input().split())) # N: 행렬 크기 M: 찾아야 할 글자 갯수
    text = [] 
    for a in range(0,N):
        text.append(input()) #입력 글자 값
    ans = ""
    for a in range(0,N): # 가로일 경우나 세로일 경우나 결국 N번의 행 또는 열을 돌아야 한다.
        for b in range(0,N-M+1): # 가로일 경우, 행의 제한을 세로일 경우 가로에 제한을 두기 위한 구문.
            check1 = True
            check2 = True
            mid = 0  # while 구문안에서 반으로 나눠서 확인을 해야하고, 이때 mid값을 기준으로 사용한다.
            while mid <= M // 2: # 만약 mid값이 절반보다 작아지면, 같은 작업은 반복하므로 더 이상 진행하지 않음
                if text[a][b+mid] != text[a][b+M-1-mid]: #가로줄 확인
                    check1 = False # 확인해서 틀리면 false
                if text[b+mid][a] != text[b+M-1-mid][a]: #세로줄 확인
                    check2 = False
                mid += 1
            if (check1 == True) or (check2 == True): # 최종적으로 true라는건 결국 맞는 값이 있다는 소리.
                if check1 == True:
                    ans = text[a][b:b+M]
                else:
                    for c in range(0,M):
                        ans += text[b+c][a]
                break # 더이상 2번째 for 구문을 실행하지 않음.
        if (check1 == True) or (check2 == True):
            break # 맞는 값이 있다면 1번째 for 구문을 실행하지 않음.
    print("#{} {}".format(T,ans))

```