---
title: gleam언어 맛보기2
published: 2024-05-30
description: gleam에서 변수선언 방법과 많이쓰는 데이터타입 알아보기
image: thumb.jpg
tags: [gleam, type, 글램, 타입]
category: gleam
draft: false
---
# gleam맛보기2
기초 문법
모든 코드에서 `main`함수와 `import gleam/io`는 생략한다.
# 변수 선언
gleam에서 변수를 선언하는 방법은 `Python`, `Rust`와 비슷하고 아주 쉽다.
```gleam
let 변수명: 타입 = 값
```


## 사칙연산(숫자 타입)
gleam의 숫자 타입에 관해 알아보자<br/>
gleam에는 숫자 타입이 `Int`와 `Float`이 있다.<br/>
`python`, `rust`, `java`, `js`, `c/c++`과 같은 언어에서는 Int와 Float은 그냥 소숫정 이후가 존재하는지 아닌지로 나눠저는데, 이 언어는 연산자도 다르다.


```gleam
let a: Int = 3
let b: Int = 4
io.debug(a + b)
io.debug(a - b)
io.debug(a * b)
io.debug(a / b)
io.debug(a % b)

let a: Float = 3.1
let b: Float = 4.1
io.debug(a +. b) // ━┓
io.debug(a -. b) //  ┃
io.debug(a *. b) //  ┠─ 연산자 뒤에 "."이 들어간다.
io.debug(a /. b) //  ┃
io.debug(a %. b) // ━┛
```

## 문자열 타입
문자열 타입은 `String`하나를 사용한다 ~~다행히도 Rust처럼 여러개가 있지는 않았다.~~
```gleam
let a: String = "1"
let a: String = "1"
io.debug(a)
```

## 불리언 타입
bool 타입은 `True`와 `False`로 나눠저있는 타입이다.
```gleam
let b: Bool = True
io.debug(b)
```


## 리스트 타입
리스트는 `List(T)`으로 타입을표기하며 `[1, 2, 3]`처럼 저장할수 있다
```gleam
let arr: List(T) = [1, 2, 3]
io.debug(arr)
```

## 튜플타입
튜플은 `#(T1, T2, T...)`으로 타입을표기하며 `#(1, 2, "a")`처럼 저장할수 있다
```gleam
let tup: #(Int, Int, String) = #(1, 2, "a")
io.debug(tup)
```

# 다음에 할꺼
다음에는 타입마다 사용할수 있는 기능을 알아볼것이다