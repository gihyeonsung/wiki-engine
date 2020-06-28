---
title   : Applicative
date    : 2020-06-04 11:02:51 +0900
updated : 2020-06-05 12:13:32 +0900
category: Typeclass
tags    : 
---

## Applicative란?

```haskell
class Functor f => Applicative (f :: * -> *) where
  pure :: a -> f a
  (<*>) :: f (a -> b) -> f a -> f b
```

Effectful한 계산을 만들 수 있는 타입이 만족할 수 있는 타입클래스이다. 다시 말해 영향이 있는 계산(Computation)에서의 함수를 적용을 추상화하는 타입클래스이다.

비슷하게 문맥 속에서 계산을 이어가는 것은 모나드와 비슷하나, 모나드보다는 약하다. 그리고 그런 이유로 더 흔하게 볼 수 있다.

`$`와 `<*>`의 타입을 비교해보면 이해하기 쉽다.

```haskell
($)   ::   (a -> b) ->   a ->   b
(<*>) :: f (a -> b) -> f a -> f b
```

위 타입 시그니쳐에서 `f`가 순수하지 않고, 영향(`f`)을 가졌음을 나타내는 것을 제외하면, 다른 타입은 같은 것을 볼 수 있다.

어떤 관점으로 보면 `pure`와 `<*>`는 `fmap`를 더 작은 단위로 나는 것과 같다. (`fmap g x = pure g <*> x`)


## 법칙

Applicative를 만족하기 위해서 지켜야 할 것이 있다. 이는 `pure`가 순수하다는 것을 어느 정도 보장하기도 한다.

아래 법칙들이 전부 만족되면, 첫 계산에서만 `pure`를 사용하는 정규화된 형태로 변환할 수 있다: `pure f <*> a <*> b <*> ...`

### Identity: `pure id <*> v = v`

### Homomorphism: `pure f <*> pure a = pure (f a)`

순수한 함수와 값을 임의로 계산 문맥에 담는 것이, 그 결과를 나중에 담는 것과 같음을 나타낸다.

여러 `pure`를 하나로 합칠 수 있게 된다.

### Interchange: `u <*> pure y = pure ($ y) <*> u`

`y`는 순수한 값이다. 이처럼 순수 함수는 `pure`를 이용해 문맥에 들어가도, 계산의 순서에 영향이 없어야 하는 것을 나타낸다.

`pure`를 좌로 욺길 수 있게 된다.

### Composition: `u <*> (v <*> w) = pure (.) <*> u <*> v <*> w`

결합 방향을 바꿀 수 있게 된다.

## 더 볼거리

- [http://www.staff.city.ac.uk/~ross/papers/Applicative.html](http://www.staff.city.ac.uk/~ross/papers/Applicative.html)
- [http://comonad.com/reader/2012/abstracting-with-applicatives/](http://comonad.com/reader/2012/abstracting-with-applicatives/)
