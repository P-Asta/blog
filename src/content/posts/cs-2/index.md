---
title: 팩토리 패턴
published: 2024-06-11
description: 팩토리 디자인패턴을 알아보자
image: thumb.jpg
tags: [design pattern, factory, 디자인 패턴, 팩토리패턴]
category: cs
draft: false
---
# 팩토리 패턴(Factory Pattern)
이 패턴은 객체 생성 로직을 캡슐화하는것을 목적으로 합니다.<br/>
이를 통해 구체적인 클래스 이름을 몰라도 객체를 생성할 수 있으며,<br/>
객체 생성 로직을 중앙에서 관리할 수 있어 코드의 유연성과 재사용성을 높일 수 있습니다.

## 예시
```rs
trait Shape {
    fn draw(&self);
}

struct Circle;
struct Square;

impl Shape for Circle {
    fn draw(&self) {
        println!("Drawing Circle");
    }
}

impl Shape for Square {
    fn draw(&self) {
        println!("Drawing Square");
    }
}
enum ShapeType {
    Circle,
    Square
}
struct ShapeFactory;

impl ShapeFactory {
    fn get_shape(shape_type: ShapeType) -> Option<Box<dyn Shape>> {
        match shape_type {
            ShapeType::Circle => Some(Box::new(Circle)),
            ShapeType::Square => Some(Box::new(Square))
        }
    }
}

fn main() {
    let shape1 = ShapeFactory::get_shape(ShapeType::Circle).unwrap();
    shape1.draw();

    let shape2 = ShapeFactory::get_shape(ShapeType::Square).unwrap();
    shape2.draw();
}
```
:::note[note]
[실행해보기](https://play.rust-lang.org/?version=stable&mode=debug&edition=2015&gist=b942b76b25badf166d6d693965724469)
:::


## 장점
- 객체 생성(constructor) 로직이 때어저 있기 때문에 보수정이 증가한다.
- 인스턴스 생성방식을 몰라도 되게때문에 더 많은 유연성을 가지게 된다.
nixos btw