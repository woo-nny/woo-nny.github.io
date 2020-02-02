---
layout: page
title: List - 부분집합의 합
description: >
  List
hide_description: true
---
## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

1부터 12까지의 숫자를 원소로 가진 집합 A가 있다. 집합 A의 부분 집합 중 N개의 원소를 갖고 있고, 원소의 합이 K인 부분집합의 개수를 출력하는 프로그램을 작성하시오.
해당하는 부분집합이 없는 경우 0을 출력한다. 모든 부분 집합을 만들어 답을 찾아도 된다.
예를 들어 N = 3, K = 6 경우, 부분집합은 { 1, 2, 3 } 경우 1가지가 존재한다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  ( 1 ≤ T ≤ 50 )
테스트 케이스 별로 부분집합 원소의 수 N과 부분 집합의 합 K가 여백을 두고 주어진다. ( 1 ≤ N ≤ 12, 1 ≤ K ≤ 100 )

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
test = int(input())
arr = [1,2,3,4,5,6,7,8,9,10,11,12]
lst =[]
#전체 부분집합을 만드는 코드.
for i in range(1<<len(arr)): #1<<n : 부분 집합의 개수
    sub_lst = []
    for j in range(len(arr)): #원소의 수 만큼 비트를 비교함
        if i&(1<<j): # i의 j번째 비트가 1이면 j번째 원소 출력
            sub_lst.append(arr[j])
    lst.append(sub_lst)

#전체 부분집합을 확인 하는 코드.
for n in range(test):
    N, K = map(int,input().split())
    #길이 맞는 리스트 구하기
    len_lst = []
    for i in lst:
        if len(i) == N:
            len_lst.append(i)


    #합 일치 유무 확인
    result = 0
    for i in len_lst:
        if sum(i) == K:
            result += 1

    print('#%s %d'%(n+1, result))
```

```python
A = list(range(1,13))
lis = []
for a in range(1 << len(A)):
    num = 0
    sums = 0
    for b in range(len(A)): #리스트의 모든 경우의 수를 구한다.
        if a & (1 << b):
            num += 1 #부분집합의 갯수가 늘어 날때마다 1씩 더해주고
            sums += A[b] # 해당하는 숫자를 sums에 더해준다.
    lis.append([num,sums]) #만들어진 num과 sums를 리스트에 추가.
sorted(lis)#정렬
T = int(input())
for test in range(1,T+1): #최종적으로 조건과 부합하는 것을 확인.
    N, K = map(int, input().split())
    cnt = lis.count([N,K])
    print("#{} {}".format(test,cnt))
```