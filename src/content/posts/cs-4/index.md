---
title: 옵저버 패턴
published: 2024-06-13
description: 옵저버 디자인패턴을 알아보자
image: thumb.jpg
tags: [design pattern, observer, 디자인 패턴, 전략패턴]
category: cs
draft: false
---
# 옵저버 패턴(Observer Pattern)
특정 값(state)가 변경됐는지 관찰을 하고, 값이 수정이 됐다면 이벤트를 발생시키는 패턴입니다.

## 쓰는곳
이 패턴은 FE에서 매우많이 쓰입니다.<br/>
`react`, `leptos`, `vue`같은 프레임워크의 State가 Observer패턴을 사용해 만들어젔고,<br/>
프로그램에서 알림을 보내는것도 옵저버 패턴이라고 할 수 있다.


## 예시코드
```rs
trait Observer<T> {
    fn update(&self, state: T);
}

struct Subject<T: Default + Clone> {
    observers: Vec<Box<dyn Observer<T>>>,
    state: T,
}

impl<T: Default + Clone> Subject<T> {
    fn new() -> Self {
        Subject {
            observers: Vec::new(),
            state: T::default(),
        }
    }

    fn attach(&mut self, observer: Box<dyn Observer<T>>) {
        self.observers.push(observer);
    }

    fn set_state(&mut self, state: T) {
        self.state = state;
        self.notify();
    }

    fn notify(&self) {
        for observer in &self.observers {
            observer.update(self.state.clone());
        }
    }
}

impl Observer<i32> for i32 {
    fn update(&self, state: i32) {
        println!("Changed State: {} -> {}", self, state);
    }
}

fn main() {
    let mut subject = Subject::new();

    let observer1 = Box::new(10);
    let observer2 = Box::new(2);
    subject.attach(observer1);
    subject.attach(observer2);

    subject.set_state(1);
}
```
:::note[실행]
[클릭하여 실행](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=c724807ec5742cdc94c6e4d0057c4140)
:::

## 장점
- 이벤트 처리시 객채를 독립적으로 동작하게 할수 있다.