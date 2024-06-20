---
title: Dialog를 사용해서 있어보이는 모달 만들기
published: 2024-06-20
description: js를 거의 사용하지 않고 css만 사용할꺼에요!
image: thumb.jpg
tags: [gleam, type, 글램, 타입]
category: gleam
draft: false
---
# DIALOG
코드는 아래 있습니다 (<button id="open"><code>클릭하여 모달 열기</code></button>)

<dialog id="modal">
    <form method="dialog">
        <label for="name">Hello World</label>
        <button>:D</button>
    </form>
</dialog>



## @starting-style
태그가 생성됐을때 절대적인 스타일입니다. transition의 영향을 받지 않습니다.

## Transition-behavior
`transition-behavior: allow-discrete`을 사용하면 `display: none`에서 다른거로 바뀔때도 transition을 적용할수 있게 도와줍니다.


## 뒷배경을 눌러 모달 닫기
모달이 열렸을때 뒤에 있는 노드(배경)의 이름이 `DIALOG`이기 떄문에 그걸 이용해 끄게 할수 있습니다.
```js
modal.addEventListener('click', (event) => {
    if (event.target.nodeName === 'DIALOG') { modal.close() }
});
```

<button id="open"><code>클릭하여 모달 열기</code></button>

<details>
<summary> 코드 보기</summary>

```html
<dialog id="modal">
    <form method="dialog">
        <label for="name">Hello World</label>
        <button>:D</button>
    </form>
</dialog>

<!-- 버튼: 모달 열기 클릭 -->
<button id="open">클릭하여 모달 열기</button>
<script>
    // 요소 ID로 가져오기
    let a = document.getElementById("open")
    let modal = document.getElementById("modal")
    // 열기 버튼에 클릭 이벤트 리스너 추가
    a.addEventListener("click", () => modal.showModal())
    // 모달 외부 클릭 시 모달 닫기 이벤트 리스너 추가
    modal.addEventListener('click', (event) => {
        if (event.target.nodeName === 'DIALOG') { modal.close() }
    });

</script>

<style>
    /* 기본 클릭 스타일 */
    .primary-click {
        color: #0062ff;
        transition: background-color 0.2s, transform 0.2s;
        cursor: pointer;
        border-radius: 4px;
        &:hover {
            background-color: #0062ff5b;
        }
        &:active {
            transform: scale(0.98);
        }
    }
    /* 다이얼로그 기본 스타일 */
    dialog {
        position: absolute;
        background-color: #fff;
        width: 400px;
        height: 200px;
        opacity: 0;
        transition: all .5s;
        transform: translateX(-40%) translateY(-50%);
        top: 50%;
        left: 50%;
        border-radius: 8px;
        border: 0;

        /* 다이얼로그 내부 버튼 스타일 */
        > form > button {
            margin-top: 16px;
            font-size: 16px;
            padding: 8px;
            border-radius: 4px;
            background-color: #0062ff27;
            font-weight: bold;
            border: 0;
            cursor: pointer;
        }
        transition-behavior: allow-discrete;
        &::backdrop {
            opacity: 0;
            transition: all .5s allow-discrete;
        }  
    }

    /* 다이얼로그 열림 상태 스타일 */
    dialog[open] {
        @starting-style {
            opacity: 0;
            transform: translateX(-50%) translateY(-60%);
            &::backdrop {
                opacity: 0;
            }
        }
        opacity: 1;
        transform: translateX(-50%) translateY(-50%);
        &::backdrop {
            opacity: 1;
        }
    }
    /* 폼 스타일 */
    form {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 100%;
        height: 100%;
        max-width: 800px;
        padding: 20px;
        border-radius: 4px;
    }
</style>
```
</details>

<script>
    let a = document.getElementById("open")
    let modal = document.getElementById("modal")
    a.addEventListener("click", () => modal.showModal())
    modal.addEventListener('click', (event) => {
        if (event.target.nodeName === 'DIALOG') { modal.close() }
    });
document.body.innerHTML += `
<style>
    .primary-click {
        color: #0062ff;
        transition: background-color 0.2s, transform 0.2s;
        cursor: pointer;
        border-radius: 4px;
        &:hover {
            background-color: #0062ff5b;
        }
        &:active {
            transform: scale(0.98);
        }
    }
    dialog {
        position: absolute;
        background-color: #fff;
        width: 400px;
        height: 200px;
        opacity: 0;
        transition: all .5s;
        transform: translateX(-40%) translateY(-50%);
        top: 50%;
        left: 50%;
        border-radius: 8px;
        border: 0;

        > form > button {
            margin-top: 16px;
            font-size: 16px;
            padding: 8px;
            border-radius: 4px;
            background-color: #0062ff27;
            font-weight: bold;
            border: 0;
            cursor: pointer;
        }
        transition-behavior: allow-discrete;
        &::backdrop {
            opacity: 0;
            transition: all .5s allow-discrete;
        }  
    }

    dialog[open] {
        @starting-style {
            opacity: 0;
            transform: translateX(-50%) translateY(-60%);
            &::backdrop {
                opacity: 0;
            }
        }
        opacity: 1 !important;
        transform: translateX(-50%) translateY(-50%);
        &::backdrop {
            opacity: 1;
        }
    }
    form {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 100%;
        height: 100%;
        max-width: 800px;
        padding: 20px;
        border-radius: 4px;
    }
    </style>
`
</script>
