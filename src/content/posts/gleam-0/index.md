---
title: gleam언어 맛보기
published: 2024-03-16
description: 초기화 및 실행
image: thumb.jpg
tags: [gleam, 글램]
category: gleam
draft: false
---
# gleam맛보기

gleam은 erlang환경에서 돌아가는 언어다(elixir처럼)


## gleam install
- window
```fish
scoop install gleam
```

- mac
```
brew install gleam
```

- linux
```
nix profile install gleam
```


## 초기화
name이라는 폴더에 gleam프로젝트가 만들어진다
```
gleam new <name>
```

## 이제 실행을 해봐야한다.
이 명령어를 쓰면 hello for <name>이 출력될꺼다.
```
cd <아까 쓴 name>
gleam run
```