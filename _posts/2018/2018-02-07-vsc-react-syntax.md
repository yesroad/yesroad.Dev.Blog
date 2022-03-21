---
title: VSCode(Visual Studio Code)에서 React JSX 자동완성 기능 활성화하기
date: 2018-02-07 15:40:00 +0900
toc: false
tags:
    - VSCode
---

WebStorm을 쓰다가 Visual Studio Code를 사용하니 React를 쓰기에 불편함이 한두가지가 아니다.

제일 처음 맞은 불편함이 JSX에서 emmet 자동완성이 작동 안되는 것인데,    
해결 방법으로 여러 방법이 있었지만 제일 간단한 방법은 아래와 같다.

기본 설정에서 아래 코드를 추가해준다.

```json
{
    "files.associations": {
        "*.js": "javascriptreact"
    }
}
```

---
References
: [Change language to JSX in Visual Studio Code
](https://stackoverflow.com/questions/32832264/change-language-to-jsx-in-visual-studio-code)
