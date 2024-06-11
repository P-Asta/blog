---
title: 펙토리 패턴
published: 2024-06-11
description: 팩토리 디자인패턴을 알아보자
image: thumb.jpg
tags: [design pattern, factory, 디자인 패턴, 팩토리패턴]
category: cs
draft: false
---
# 펙토리 패턴(Factory Pattern)
이 패턴은 객체 생성 로직을 캡슐화하는것을 목적으로 합니다.<br/>
이를 통해 구체적인 클래스 이름을 몰라도 객체를 생성할 수 있으며,<br/>
객체 생성 로직을 중앙에서 관리할 수 있어 코드의 유연성과 재사용성을 높일 수 있습니다.

## 예시
```rs
fn main() {
    print_sound(Suv);
    print_sound(Sedan);
    print_sound(Truck);
}

fn print_sound(car: impl Car) {
    car.sound();
}

struct Suv;
struct Sedan;
struct Truck;

trait Car {
    fn sound(&self) {
        println!("Vroom!")
    }
}

impl Car for Suv {}
impl Car for Sedan {
    fn sound(&self) {
        println!("Vroom! Vroom!")
    }
}
impl Car for Truck {
    fn sound(&self) {
        println!("Vroom! Vroom! Vroom!")
    }
}
```
:::note[note]
[실행해보기](https://play.rust-lang.org/?version=stable&mode=debug&edition=2015&code=fn+main%28%29+%7B%0A++++print_sound%28Suv%29%3B%0A++++print_sound%28Sedan%29%3B%0A++++print_sound%28Truck%29%3B%0A%7D%0A%0Afn+print_sound%28car%3A+impl+Car%29+%7B%0A++++car.sound%28%29%3B%0A%7D%0A%0Astruct+Suv%3B%0Astruct+Sedan%3B%0Astruct+Truck%3B%0A%0Atrait+Car+%7B%0A++++fn+sound%28%26self%29+%7B%0A++++++++println%21%28%22Vroom%21%22%29%0A++++%7D%0A%7D%0A%0Aimpl+Car+for+Suv+%7B%7D%0Aimpl+Car+for+Sedan+%7B%0A++++fn+sound%28%26self%29+%7B%0A++++++++println%21%28%22Vroom%21+Vroom%21%22%29%0A++++%7D%0A%7D%0Aimpl+Car+for+Truck+%7B%0A++++fn+sound%28%26self%29+%7B%0A++++++++println%21%28%22Vroom%21+Vroom%21+Vroom%21%22%29%0A++++%7D%0A%7D%0A)
:::


## 장점
- 객체 생성(constructor) 로직이 때어저 있기 때문에 보수정이 증가한다.
- 인스턴스 생성방식을 몰라도 되게때문에 더 많은 유연성을 가지게 된다.
nixos btw