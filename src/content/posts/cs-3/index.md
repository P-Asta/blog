---
title: 전략 패턴
published: 2024-06-12
description: 전략 디자인패턴을 알아보자
image: thumb.jpg
tags: [design pattern, strategy, 디자인 패턴, 전략패턴]
category: cs
draft: false
---
# 전략 패턴(Strategy Pattern)
이 패턴은 [팩토리 패턴](../cs-2/)과 비슷합니다.
캡슐화를 하며, 실행 코드를 서로 공유하는것을 목적으로합니다.

## 예시
```rs
trait Shape {
    fn draw(&self);
}

struct Circle;
struct Square;

impl Shape for Circle {
    // draw알고리즘
    fn draw(&self) {
        println!("Drawing Circle");
    }
}

impl Shape for Square {
    // draw알고리즘
    fn draw(&self) {
        println!("Drawing Square");
    }
}
struct Context {
    shape: &'static dyn Shape,
}

impl Context {
    fn new(shape: &'static dyn Shape) -> Self {
        Self { shape }
    }
    fn draw(&self) {
        self.shape.draw();
    }
}

fn main() {
    let ctx1 = Context::new(&Circle);
    ctx1.draw();
    let ctx2 = Context::new(&Square);
    ctx2.draw();
}
```
:::note[note]
[실행해보기](https://play.rust-lang.org/?version=stable&mode=debug&edition=2015&gist=b1800d828ddb121e054ebf2bdc6d5a82)
:::


## 장점
- 알고리즘 변경이 쉬워 유연하게 작업할수 있다.
- 각각의 알고리즘을 쉽게 테스트할수 있어 유연하다.