---
layout: page
title: List
description: >
  List
hide_description: true
---

~~~python
num = int(input())
res=num *[0]
ans=num*[0]
for i in range(num):    
    count = int(input())
    number=input().split()
    res[i] = list(map(int, number))
    ans[i]=max(res[i])-min(res[i])

for i in range(num):
    print("#{} {}".format(i+1,ans[i]))
~~~