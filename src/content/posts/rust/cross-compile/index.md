---
title: 러스트 크로스 컴파일하기
published: 2024-06-20
description: js를 거의 사용하지 않고 css만 사용할꺼에요!
image: thumb.jpg
tags: [rust, cross-compile, 러스트, 크로스-컴파일]
category: gleam
draft: false
---
# 크로스 컴파일
크로스 컴파일은 자신의 Os에서 다른Os로 컴파일을 해주는거다.

## cross-rs설치
러스트에서 크로스 컴파일을 쉽게 하기위해 `cross-rs`라는것을 설치해줍니다.
```shell
cargo install cross --git https://github.com/cross-rs/cross
```
:::important
cross는 docker를 사용하기떄문에 [docker공식 페이지](https://docs.docker.com/engine/install)또는 페키지 매니저를 사용해서 설치해줍니다.
:::


## cross compile
아래있는거 이외의것은 `rustup target list`명령어를 사용하여 확인할수 있다.
```shell
# linux complie
cross build --target aarch64-unknown-linux-gnu --release
# windows complie
cross rustc --target x86_64-pc-windows-gnu --release
```
wine을 사용해서 실행해보니 성공 :D
![alt text](image.png)
