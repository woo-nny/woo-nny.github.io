---
layout: page
title: Stack - 괄호 검사
description: >
  Stack
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다. 

주어진 입력에서 괄호 {}, ()가 제대로 짝을 이뤘는지 검사하는 프로그램을 만드시오.
예를 들어 {( )}는 제대로 된 짝이지만, {( })는 제대로 된 짝이 아니다. 입력은 한 줄의 파이썬 코드일수도 있고, 괄호만 주어질 수도 있다.
정상적으로 짝을 이룬 경우 1, 그렇지 않으면 0을 출력한다.
print(‘{‘) 같은 경우는 입력으로 주어지지 않으므로 고려하지 않아도 된다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤50
다음 줄부터 테스트 케이스 별로 온전한 형태이거나 괄호만 남긴 한 줄의 코드가 주어진다.

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
test = int(input())

for n in range(test):
    code = list(input())
    res = []
    for i in code:
        if i == '(' or i == '{':
            res.append(i)
        elif i == ')' or i == '}': # 닫는 괄호 이며 stack이 빈 경우 => 처음부터 닫는 괄호가 오는 경우
            if len(res) == 0:
                res = [i]
                break
            elif (i == "}" and res[-1] !="{") or (i == ")" and res[-1] != "("):  #stack에 저장된 괄호와 일치하지 않는 경우
                res = [i]
                break
            else:   #stack에 저장된 괄호와 일치하는 닫는 괄호가 오는 경우
                res.pop()
    if len(res)==0:
        ans =1
    else:
        ans =0
    print("#{} {}".format(n+1,ans))
```

```python
T = int(input())
for t in range(1,T+1):
    question = input()
    checklis = []
    ans = 1
    for a in question:
        if a =="(" or a == "{" or a== "[":
            checklis.append(a)
        elif a == ")":
            if len(checklis) == 0 or checklis.pop(-1) != "(":
                ans = 0
                break
        elif a=="}":
            if len(checklis) == 0 or checklis.pop(-1) != "{":
                ans = 0
                break
        elif a == "]":
            if len(checklis) == 0 or checklis.pop(-1) != "[":
                ans = 0
                break
    if len(checklis) != 0:
        ans = 0
    print("#{} {}".format(t,ans))
```