---
layout: page
title: List - 숫자 카드
description: >
  List
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

0에서 9까지 숫자가 적힌 N장의 카드가 주어진다.
가장 많은 카드에 적힌 숫자와 카드가 몇 장인지 출력하는 프로그램을 만드시오. 카드 장수가 같을 때는 적힌 숫자가 큰 쪽을 출력한다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  ( 1 ≤ T ≤ 50 )
다음 줄부터 테스트케이스의 첫 줄에 카드 장수 N이 주어진다. ( 5 ≤ N ≤ 100 )
다음 줄에 N개의 숫자 ai가 여백없이 주어진다. (0으로 시작할 수도 있다.)  ( 0 ≤ ai ≤ 9 ) 

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 가장 많은 카드의 숫자와 장 수를 차례로 출력한다.

~~~python
T= int(input())
for i in range(T):
    card = [0]*10 # 0~9까지 빈공간을 생성
    N = int(input())
    N_num = str(input())
    N_num = list(map(int,N_num)) #input값을 int로 변경
    for j in range(N):
        card[N_num[j]] += 1 # 카드의 숫자를 확인 후 카운트 증가
    max_index, max_num = 0, 0
    for k in range(len(card)-1,-1,-1):
        if card[k] > max_index:
            max_index = card[k]
            max_num = k
    print('#{} {} {}'.format(i+1, max_num, max_index))
~~~

~~~python
from sys import stdin
T = int(stdin.readline())
for a in range(1,T+1):
   N = int(stdin.readline())
   lis = list(map(int, stdin.readline().strip()))
   mid = 0
   cnt = 0
   for b in set(lis): # 중복된 숫자를 제거해 검사해야할 숫자집단을 만든다.
       if cnt <= lis.count(b): # 숫자 집단에서 나온 숫자를 lis에서 몇 개 있는지 카운트 한다.
           cnt = lis.count(b)
           if mid < b:
               mid = b
   print("#{} {} {}".format(a,mid,cnt))
~~~