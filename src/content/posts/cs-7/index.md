---
title: mvc / mvp / revealing module
published: 2024-07-09
description: mvc / mvp / revealing module
image: thumb.jpg
tags: [design pattern, mvc, mvp, revealing module, 디자인 패턴, 노출 모듈]
category: cs
draft: false
---
# 노출모듈 패턴(revealing module pattern)
class에서 보여주고싶은값은 보여주고 보여주기 싫은것들은 내부에서만 사용할수 있게 숨겨놓는 패턴입니다.
```rs
struct User {
    token: String, // 숨길값
    pub name: String // 보여줄값
}
```

# mvc 패턴(model view controller)
컨트롤러를 만들어놓고 특정 struct를 그 컨트롤러를 사용하여 관리하는 패턴입니다.ㄴ
```rs
// Controller
struct Controller {
    model: Model,
}

impl Controller {
    pub fn on_model_change(&self) {
        println!("Model has changed");
    }
}
// Model
struct Model<'a> {
    controller: &'a Controller,
    foo: i32,
}

impl Model {
    pub fn notify_controller_change(&self) {
        self.controller.on_model_change();
    }
}

fn main() {
    // Viewer
    let controller = Controller { model: Model { foo: 0, controller: &controller } };
}
```

# mvp 패턴(model view presenter pattern)
```rs
// Model: 기본적인 기능이 담겨있음
pub struct Counter {
    pub value: i32,
}

impl Counter {
    pub fn new() -> Self {
        Counter { value: 0 }
    }

    pub fn increment(&mut self) {
        self.value += 1;
    }

    pub fn decrement(&mut self) {
        self.value -= 1;
    }

    pub fn get_value(&self) -> i32 {
        self.value
    }
}
// View: 값을 보여줄때 사용
pub trait View {
    fn show_value(&self);
}
impl View for Counter {
    fn show_value(&self) {
        println!("{}", self.value)
    }
}

// Model과 View 상호작용
pub struct CounterPresenter {
    model: Counter,
}

impl CounterPresenter {
    pub fn new(model: Counter) -> Self {
        CounterPresenter { model }
    }

    pub fn increment(&mut self) {
        self.model.increment();
        self.model.show_value();
    }

    pub fn decrement(&mut self) {
        self.model.decrement();
        self.model.show_value();
    }
}
fn main() {
    let model = Counter::new();
    let mut presenter = CounterPresenter::new(model);

    // Simulate user interactions
    presenter.increment();
    presenter.increment();
    presenter.decrement();
}

```
