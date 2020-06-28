---
title   : LR 파서
date    : 2020-04-20 18:10:58 +0900
updated : 2020-06-04 23:24:39 +0900
category: PLT
tags    : 
---

## LR 파서

LR 파서는 좌에서 우로 읽고, 우단 우도를 하는 파서이다.

[LL 파서](LL-파서)와 마찬가지로 lookahead 기호의 개수를 이용해 `LR(K)`로 표현하며, 이 역시 보통 `LR(1)`이다.

SLR, [CLR](CLR), [LALR](LALR) 방법이 있다. 같은 방법으로 파싱하나, 파싱표가 다를 수 있다. 물론 파싱표를 만드는 방법에 따라 분석할 수 있는 문법의 범위가 달라진다.

## 파싱 알고리즘

```
repeat
  if ACTION[s, a] is sX
    push a
    push X
  else if ACTION[s, a] is rX (A -> B)
    pop |B| times
    push A
    push n when GOTO[X, A] is n
  else if ACTION[s, a] = acc
    ok
  else
    error
```
