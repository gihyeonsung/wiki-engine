---
title   : Polymorphism
date    : 2020-06-03 13:49:25 +0900
updated : 2020-06-04 23:24:45 +0900
category: PLT
tags    : 
---

## 다형성

다형성은 한 가지 인터페이스로 여러 타입의 것들을 제공하는 것이다.

## 다형성의 종류

### Parametric

Parametric polymorphism은 어떤 것이 제약되지 않은 타입을 가지고 있는 것이다. 즉 타입에 대한 정보가 아무것도 없는 것이다.

타입에 대한 아무 정보도 없기 때문에, 타입을 사용하는 것(kind가 * -> * 이상인 타입이나 함수)이 동일한 방법으로 값을 처리할 수 있고, 따라서 하나의 정의만 있을 수 있다.

OOP에서 템플릿, 제네릭으로 구현될 수 있다.

### Ad-hoc

Ad-hoc polymorphism은 타입에 대한 여러 다른 정의가 주어졌을 때, 값이 상황에 맞게 적응되는 것이다.

C++, Java 같은 언어에서는 Overloading로 지원하고, Haskell에서는 [Typeclass](Typeclass)와 instance로 구현된다.

### Subtype (inclusion)

Subtype polymorphism은 타입 간에 상속(서브타입) 관계에서 안전하게 다른 타입으로 간주될 수 있도록 해준다. 예를 들어 `S <: T`인 경우에 `S`를 `T`처럼 사용할 수 있는 것이다. 이는 리스코프 치환 원칙을 실현하도록 도와준다.

보통 Virtual table을 사용해서 구현된다.
