---
title   : Monad
date    : 2020-06-09 10:48:50 +0900
updated : 2020-06-11 15:47:55 +0900
category: Typeclass
tags    : 
---

## 모나드

```haskell
class Applicative m => Monad m where
  return :: a -> m a
  (>>=) :: m a -> (a -> m b) -> m b
  (>>) :: m a -> m b -> m b
  m >> n = m >>= \_ -> n
  
  fail :: String -> m a
```

모나드는 "이전 계산의 결과값을 이용해서 다음 계산을 만들 수 있도록 하는" 타입클래스이다.

`return`은 어떤 값을 영향이 있는 결과 값으로 취급하게 해 준다. ([Applicative](Applicative)의 `pure`와 같은 기능이다.)

`bind`(`(>>=)`)는 첫 게산(`m a`)의 영향과 결과 값을 가지고, 다음 계산을 수행하는 함수다.

`(>>)`는 Applicative의 `*>`와 같다. 두 계산을 차례로 수행하고, 두 번째 게산의 결과 값만을 취하는 것이다. (`a >> b = b`는 타입을 만족하나, 두 계산의 영향을 전부 가지되 두 번째 결과 값만 취한다는 의미적인 관점에서는 잘못된 구현이다.)

### Applicative와의 차이점

Monad와 Applicative는 여러 계산 결과를 모아 하나의 계산으로 만들 수 있는 점은 같으나, 몇 가지 차이가 있다.

#### Monad가 더 유연하다

[Applicative](Applicative)는 다음 행동을 결정할 수 없다. 이는 다음 계산을 할 수 있게 해주는 `<*>`의 타입을 보면 알 수 있다.

```haskell
(<*>) :: f (a -> b) -> f a -> f b
```

여기서 계산 `f a`은 이전에 있던 계산들에 대해서 아무런 정보를 가질 수가 없다. 이미 계산이 결정되어 있기 때문이다. 그러나 이와 달리 `bind`가 받는 `a -> m b`는 이전 계산의 값 `a`를 알고, 사용해서 다음 계산 `b`를 만들어낸다.

이처럼 두 타입클래스는 어떤 타입이 이펙트가 있는 연산을 이어갈 수 있게 해주나, Monad만이 이전 결과를 이용해 다음 계산을 만들 수 있는 것이 차이점이다.

Applicative는 이전 계산의 결과를 알 수 없다는 점을 생각하면, Applicative는 CFG를 위한 파서만 만들 수 있고, Monad를 사용해야 Context-sensitive grammer를 파싱 할 수 있는 것을 알 수 있다.

#### Monad는 순차적이다

Applicative의 `<*>`를 이용해 연결한 계산에서 값들은 그 자체로 이미 완전한 값이다. 이는 타입에도 나와있다. (`f a`) 그러나, 모나드의 `bind`로 만든 계산에서 그 요소들은 이전 연산에 영향을 받는다. (`a -> m b`). 따라서 모나드로 만들어진 계산과 달리, Applicative로 만들어진 계산은 병렬적으로 실행될 여지가 있다.

### `bind` 대신 `join :: m (m a) -> m a`로 모나드 만들기

어떤 타입이 Monad를 만족하기 위해서는, `bind`와 `return`을 할 수 있어야 한다. 그러나, `fmap`, `return` 그리고 겹쳐진 계산을 풀어주는(계산하는) `join`을 이용해서 모나드를 만족할 수도 있다.

```haskell
k (>>=) f = join (fmap f k)
```

## 더 볼거리

- [https://wiki.haskell.org/Typeclassopedia#Monad](https://wiki.haskell.org/Typeclassopedia#Monad)
- [http://blog.sigfpe.com/2007/04/trivial-monad.html](http://blog.sigfpe.com/2007/04/trivial-monad.html)
