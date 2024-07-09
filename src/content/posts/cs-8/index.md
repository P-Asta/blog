---
title: mvvm
published: 2024-07-09
description: model view view-model
image: thumb.jpg
tags: [design pattern, mvvm, 디자인 패턴]
category: cs
draft: false
---
# mvvm 패턴(model view view-model pattern)
model과 view를 분리해놓고 view-model에서 다 처리하는 패턴이다
```rs
// models.rs
pub struct User {
    pub name: String,
    pub age: u32,
}

impl User {
    pub fn new(name: &str, age: u32) -> Self {
        User {
            name: name.to_string(),
            age,
        }
    }
}

// views.rs
pub struct UserView;

impl UserView {
    pub fn display_user(&self, name: &str, age: u32) {
        println!("User Name: {}", name);
        println!("User Age: {}", age);
    }

    pub fn prompt_user_input(&self) -> (String, u32) {
        use std::io::{self, Write};

        let mut name = String::new();
        let mut age = String::new();

        print!("Enter user name: ");
        io::stdout().flush().unwrap();
        io::stdin().read_line(&mut name).unwrap();

        print!("Enter user age: ");
        io::stdout().flush().unwrap();
        io::stdin().read_line(&mut age).unwrap();

        let age: u32 = age.trim().parse().expect("Invalid age input");

        (name.trim().to_string(), age)
    }
}

pub struct UserViewModel {
    user: User,
    view: UserView,
}

impl UserViewModel {
    pub fn new(user: User, view: UserView) -> Self {
        UserViewModel { user, view }
    }

    pub fn update_user(&mut self, name: String, age: u32) {
        self.user.name = name;
        self.user.age = age;
    }

    pub fn show_user(&self) {
        self.view.display_user(&self.user.name, self.user.age);
    }

    pub fn get_user_input_and_update(&mut self) {
        let (name, age) = self.view.prompt_user_input();
        self.update_user(name, age);
    }
}

```