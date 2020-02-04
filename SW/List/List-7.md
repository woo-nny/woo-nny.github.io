---
layout: page
title: List - 부분집합의 합
description: >
  List
hide_description: true
comments: true
---
## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

코딩반 학생들에게 이진 탐색을 설명하던 선생님은 이진탐색을 연습할 수 있는 게임을 시켜 보기로 했다.

짝을 이룬 A, B 두 사람에게 교과서에서 각자 찾을 쪽 번호를 알려주면, 이진 탐색만으로 지정된 페이지를 먼저 펼치는 사람이 이기는 게임이다.

예를 들어 책이 총 400쪽이면, 검색 구간의 왼쪽 l=1, 오른쪽 r=400이 되고, 중간 페이지 c= int((l+r)/2)로 계산한다.

찾는 쪽 번호가 c와 같아지면 탐색을 끝낸다.

A는 300, B는 50 쪽을 찾아야 하는 경우, 다음처럼 중간 페이지를 기준으로 왼쪽 또는 오른 쪽 영역의 중간 페이지를 다시 찾아가면 된다.
![list7](../image/4.jpeg)
책의 전체 쪽수와 두 사람이 찾을 쪽 번호가 주어졌을 때, 이진 탐색 게임에서 이긴 사람이 누구인지 알아내 출력하시오. 비긴 경우는 0을 출력한다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1<=T<=50
테스트 케이스 별로 책의 전체 쪽 수 P, A, B가 찾을 쪽 번호 Pa, Pb가 차례로 주어진다. 1<= P, Pa, Pb <=1000
 

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, A, B, 0 중 하나를 출력한다.

```python
# case 1개 실패
def binarySearch(a,key):
    start  = 0
    end = a
    count =0
    while start<=end:
        middle = start +(end-start)//2
        if key == middle: #검색 성공
         return count
        elif key <middle:
            end = middle
            count += 1
        else:
            start =middle
            count += 1
    return count #검색 실패
test = int(input())

for n in range(test):
    P, A, B = map(int,input().split())
    if binarySearch(P,A)<binarySearch(P,B):
        print("#{} A".format(n+1))
    elif binarySearch(P,A)>binarySearch(P,B):
        print("#{} B".format(n+1))
    elif binarySearch(P,A)==binarySearch(P,B):
        print("#{} 0".format(n+1))
```
```python
# case 1개 실패
def binary(start,end,purpose,cnt):
    center = (start + end)//2
    if center == purpose:
        return cnt
    else:
        if purpose > center:
            start = center + 1
            cnt += 1
            return binary(start, end, purpose,cnt)
        else:
            end = center - 1
            cnt += 1
            return binary(start, center, purpose,cnt)
            
T = int(input())
for t in range(1,T+1):
    P,A,B = map(int, input().split())
    Acnt = binary(1, P, A, 1)
    Bcnt = binary(1, P, B, 1)
    if Acnt > Bcnt:
        print("#{} {}".format(t,"A"))
    elif Acnt < Bcnt:
        print("#{} {}".format(t,"B"))
    else:
        print("#{} {}".format(t,"0"))
```

