---
layout: page
title: String - 문자열 비교
description: >
  String
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

두 개의 문자열 str1과 str2가 주어진다. 문자열 str2 안에 str1과 일치하는 부분이 있는지 찾는 프로그램을 만드시오.
예를 들어 두 개의 문자열이 다음과 같이 주어질 때, 첫 문자열이 두번째에 존재하면 1, 존재하지 않으면 0을 출력한다.
ABC
ZZZZZABCZZZZZ
두번째 문자열에 첫번째 문자열과 일치하는 부분이 있으므로 1을 출력.
ABC
ZZZZAZBCZZZZZ
문자열이 일치하지 않으므로 0을 출력.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  (1≤T≤50)
다음 줄부터 테스트 케이스 별로 길이가 N인 문자열 str1과 길이가 M인 str2가 각각 다른 줄에 주어집니다. (5≤N≤100, 10≤M≤1000, N≤M)

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
test = int(input())

for n in range(test):
    str1 = input() #첫번째 입력
    str2 = input() #두번째 입력
    result = 0
    for i in range(len(str2)-len(str1)+1): 
        if str2[i:i+len(str1)] == str1: #슬라이스를 통해 처음부터 첫번째 입력 길이만큼 서로 비교
            result = 1
    print('#{} {}'.format(n+1, result))
```

```python
#보이어무어 알고리즘 비슷
T = int(input())
for t in range(1,T+1):
    str1 = input()
    str2 = input()
    rstr1 = list(reversed(str1)) #
    a = len(str1)
    ans = 0
    
    check = True
    while a <= len(str2):
        if str1 == str2[a-len(str1):a]:
            ans = 1
            break
        else :
            if rstr1[0] == str2[a-1]:
                a += 1
            else:
                try:
                    a += rstr1.index(str2[a-1])
                except:
                    a += len(str1)
    print("#{} {}".format(t,ans))
```