---
title   : FOLLOW
date    : 2020-04-17 10:16:16 +0900
updated : 2020-06-04 23:24:20 +0900
category: PLT
tags    : 
---

## FOLLOW(A)란

문맥 자유 문법에서 `A` 다음에 따라올 수 있는 터미널의 집합이다. 계산하기 위해서 [FIRST](FIRST)를 알고 있어야 한다.

## 필요성

[FIRST](FIRST)와 마찬가지로 예측을 위해서 사용되나, FIRST만으로는 예측이 불가능할 때 사용된다.

## 계산하는 방법

`FOLLOW(A)`를 계산하는 방법은 아래 규칙을 사용한다.

1. `FOLLOW(S) = $`이다.
2. `A -> aBb`이면, `FOLLOW(B)`는 공문자열을 제외한 `FIRST(b)`의 부분집합이다.
3. `A -> aB`이거나 `A -> aBb`에서 b가 nullable 하면, `FOLLOW(A)`는 `FOLLOW(B)`의 부분 집합이다.

## 같이 보기

- [FIRST](FIRST)
