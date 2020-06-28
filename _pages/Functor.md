---
title   : Functor
date    : 2020-05-31 16:05:48 +0900
updated : 2020-06-04 23:24:24 +0900
category: Typeclass
tags    : 
---

## Functor란?

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

Functor는 kind가 `* -> *`가 구현할 수 있는 타입클래스다. (`[]`, `Maybe`, ...)

## Functor의 이해

Functor를 구현하는 타입은 아래 두 관점으로 볼 수 있다.

- 요소에 같은 방법으로 함수를 적용할 수 있는 컨테이너.
- 계산 문맥 (Computational context)

`fmap`이 curry 되었다는 것을 알면, `fmap`이 일반 함수를 특정 문맥 안에서 적용되도록 "`lift` 한다"고 바라볼 수도 있다. (`fmap :: (a -> b) -> (f a -> f b)`)

## Functor의 특징

두 관점 전부, 이상적인 `fmap`은 문맥(자료의 구조)을 바꾸지 않고, 가지고 있는 자료만 바꾼다. 더 정확하게는 이상적인 fmap은 아래 두 규칙을 지킨다.

```haskell
fmap id = id
fmap (g . h) = fmap g . fmap h
```

여기서 첫 번째 규칙을 지키면, Haskell에서 `seq`와 `undefined`를 제외하고 자동으로 두 번째 규칙도 참이 된다.

Functor는 다른 타입과 달리, free theorem에 의해 위 규칙을 만족하는 구현은 최대 하나라는 것을 증명할 수 있다.

## "`* -> *`이지만, Functor를 만족할 수 없는 타입이 있다."

문맥/컨테이너와 같이 값을 가지고 있으나, `g :: a -> b`인 함수를 적용할 수 없는 타입은 Functor를 구현할 수 없다.

```haskell
newtype T a = T (a -> Integer)
```

타입 `T`에 대해서 Functor의 인스턴스를 구현하면 아래 시그니쳐가 된다.

```haskell
fmap :: (a -> b) -> T a -> T b
```

이를 구체적으로 풀어보면, `a -> b`와 `a -> Integer`를 이용해 `b -> Integer`인 함수를 만들 수 있어야 한다.

그러나 `a -> b`와 `a -> Integer`를 이용해 타입 `b`가 타입 `Integer`에 도달할 수 있는 방법이 없다. 

![functor]({{ site.media }}/Functor/functor.svg)

따라서, 어떤 타입에 대해서 Functor를 구현할 수 없는 것은 참이다.

## 링크 

- [https://wiki.haskell.org/Typeclassopedia#Functor](https://wiki.haskell.org/Typeclassopedia#Functor)
- [https://stackoverflow.com/questions/26985562/make-data-type-of-kind-thats-not-a-functor](https://stackoverflow.com/questions/26985562/make-data-type-of-kind-thats-not-a-functor)
