---
layout: page
title: String - 글자수
description: >
  String
comments: true
hide_description: true
---

## ※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.

두 개의 문자열 str1과 str2가 주어진다. 문자열 str1에 포함된 글자들이 str2에 몇 개씩 들어있는지 찾고, 그중 가장 많은 글자의 개수를 출력하는 프로그램을 만드시오.
예를 들어 str1 = “ABCA”, str2 = “ABABCA”인 경우, str1의 A가 str2에 3개 있으므로 가장 많은 글자가 되고 3을 출력한다.
파이썬의 경우 딕셔너리를 이용할 수 있다.

[입력]
첫 줄에 테스트 케이스 개수 T가 주어진다.  1≤T≤50
다음 줄부터 테스트 케이스 별로 길이가 N인 문자열 str1과 길이가 M인 str2가 각각 다른 줄에 주어진다. 5≤N≤100, 10≤M≤1000, N≤M

[출력]
각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

```python
test = int(input())

for n in range(test):
    str1 = input()
    str2 = input()
    sub_cnt, cnt = 0, 0
    for i in str1:
        for j in str2:
            if i == j: #각 각 비교
                sub_cnt += 1
        if sub_cnt > cnt: #가장 큰 cnt를 찾는 구문
            cnt = sub_cnt
        sub_cnt = 0
    print("#{} {}".format(n+1,cnt))
    
```

```python
T = int(input())
for t in range(1,T+1):
    str1 = input()
    str2 = input()
    str1Set = set(str1) # 후보군의 중복없이 만들어준다.
    zeros = [0]*len(str1Set) # 딕셔너리에 들어가기 위해 후보군의 초기값을 설정해준다.
    dic = dict(zip(str1Set,zeros)) # 위의 2개를 key값으로 strlset, values값으로 zeros로하여 딕셔너리화 한다.
    for a in str2: # 구문을 이용해 str2와
        if a in dic.keys(): # key값을 비교하고
            dic[a] += 1 # 키값과 같은 글자가 나온 경우 value의 값을 +1 해준다.
    ans = [[k, v] for k, v in dic.items() if dic[k] == max(dic.values())] # 최종적으로 딕셔너리를 확인해 최대값 구함.
    print("#{} {} {}".format(t, ans[0][0], ans[0][1]))
    
```