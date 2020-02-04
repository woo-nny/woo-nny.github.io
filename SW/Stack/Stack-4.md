---
layout: page
title: Stack - 반복문자 지우기
description: >
  Stack
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

문자열 s에서 반복된 문자를 지우려고 한다. 지워진 부분은 다시 앞뒤를 연결하는데, 만약 연결에 의해 또 반복문자가 생기면 이부분을 다시 지운다.
반복문자를 지운 후 남은 문자열의 길이를 출력 하시오. 남은 문자열이 없으면 0을 출력한다.
다음은 CAAABBA에서 반복문자를 지우는 경우의 예이다.
CAAABBA 연속 문자 AA를 지우고 C와 A를 잇는다.
CABBA 연속 문자 BB를 지우고 A와 A를 잇는다.
CAA 연속 문자 AA를 지운다.
C 1글자가 남았으므로 1을 리턴한다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤ 50
다음 줄부터 테스트 케이스의 별로 길이가 1000이내인 문자열이 주어진다.

[출력]
#과 1번부터인 테스트케이스 번호, 빈칸에 이어 답을 출력한다.


```python
test = int(input())

for n in range(test):
    code = input()
    ans =[] #남은 글자
    for c in code:
        if not ans or ans[-1] != c:
            ans.append(c)
        elif ans and ans[-1] == c: #남은 글자와 현재 글자가 같으면
            ans.pop() #pop
    print("#{} {}".format(n+1,len(ans)))
```

```python
def DelReduplication(str):
    res = []
    for a in str:
        if len(res) == 0 or a != res[-1]:
            res.append(a)
        else:
            res.pop(-1)
    return len(res) if len(str) == len(res) else DelReduplication(res)
T = int(input())
for t in range(1,T+1):
    str = list(input())
    print("#{} {}".format(t,DelReduplication(str))) 
```