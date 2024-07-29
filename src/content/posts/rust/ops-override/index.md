---
title: 연산자 오버로드
published: 2024-03-14
description: Welcome to Hugo Theme Stack
image: thumb.jpg
tags: [rust, rust-syntax, operator overload, 러스트, 러스트 문법, 연산자 오버로드]
category: rust-syntax
draft: false
---

rust에서 연산자 오버로드를 사용하려면 `std::ops`에 있는 trait을 상속 시키면 된다


아레 코드는 Vec2끼리 더하기를 가능하게 하는 코드다
```rs
use std::ops::Add;

struct Vec2 {
    x: f32,
    y: f32,
}

// Add 상속
impl Add for Vec2 {
    // 더했을때 반환할 타입
    type Output = Vec2;

        /*
        let a = Vec2{x: 1.0, y: 3.0}
        let b = Vec2{x: 1.0, y: 3.0}
        일 경우
        a + b를 했을때
        Vec2{
            x: a.x + b.x,
            y: a.y + b.y,
        }
        를 반환해주는 함수
        */
    fn add(self, rhs: Vec2) -> Vec2 {
        Vec2 {
            x: self.x + rhs.x,
            y: self.y + rhs.y,
        }
    }
}

```
덧셈 말고도 `뺄셈(Sub)` `나눔셈(Div)` `곱셈(Mul)`같은게 있고
`+=`를 구현하고싶다면 `AddAssign`을 쓰면 된다