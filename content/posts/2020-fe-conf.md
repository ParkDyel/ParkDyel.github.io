---
title: "2020 Fe Conf"
date: 2021-02-20T00:45:31+09:00
draft: false
tags: ["conf"]
---

## 트랙 A
### [A1. 웹뷰에서 다크모드 상속받기: 일관성있는 사용자 경험을 위하여](https://youtu.be/ElsZ-v4Ow08)
  - [CSS Variable](https://developer.mozilla.org/ko/docs/Web/CSS/Using_CSS_custom_properties)
    - _ie 지원 안함_
    - [prefers color scheme](https://developer.mozilla.org/ko/docs/Web/CSS/@media/prefers-color-scheme): AOS 10, iOS13 이후로 지원이 되고, 사용자가 앱만 다크모드로 쓰고 싶은 경우에는 결국 사용하기가 애매할 수 있음.
    - CSS Varialbe 예제
      ```css
      :root {
      --main-bg-color: brown;
      }

      .one {
        color: white;
        background-color: var(--main-bg-color);
        margin: 10px;
        width: 50px;
        height: 50px;
        display: inline-block;
      }

      .two {
        color: white;
        background-color: black;
        margin: 10px;
        width: 150px;
        height: 70px;
        display: inline-block;
      }
      .three {
        color: white;
        background-color: var(--main-bg-color);
        margin: 10px;
        width: 75px;
      }
      .four {
        color: white;
        background-color: var(--main-bg-color);
        margin: 10px;
        width: 100px;
      }
      ```
    - js로 CSS Variable 접근
      ```css
      .five {
        background-color: var(--main-bg-color);
      }

      // 인라인 스타일에서 변수 얻기
      element.style.getPropertyValue("--my-var");

      // 어느 곳에서나 변수 얻기 
      getComputedStyle(element).getPropertyValue("--my-var");

      // 인라인 스타일에 변수 설정하기
      element.style.setProperty("--my-var", jsVar + 4);
      ```
    - CSS Variable이 지원안되는 경우 fallbock code
      ```scss
      .adaptive-color-900 {
      	color:$grey900;
        color:var(--adaptiveGrey900);
      }
      ```
    - lightMode에서 darkMode로 전환되는 순간 흰색 화면이 나오는 버그가 있어, 사용자 경험에 좋지 않았다고 합니다. 그래서 결국 SSR 할때 동적으로 CSS를 내려주었고, 그때를 위한 캐시 정책도 소개 하고 있습니다.
    
### [A2. iframe을 활용하여 전혀 다른 Service를 통합하기](https://youtu.be/kZO5PEypjVg)
  - XSS 공격 방어를 위한 sandbox 속성 설정
  	- [속성 값](https://www.w3schools.com/tags/att_iframe_sandbox.asp)이 잘 이해가 안됨
    - 다만, allow-script와 allow-same-origin을 사용하는 경우 보안에 취약해질 수 있으므로, src에 대한 검증이 필요하다.
    
### [A4. Relay, 그리고 Declarative에 대해 다시 생각하기](https://youtu.be/YP7d9ae_VzI)
  - GraphQL과 Relay
  	- [Vue Relay](https://github.com/vue-relay/vue-relay)
    
### [A5. 프론트엔드에서 TDD가 가능하다는 것을 보여드립니다.](https://youtu.be/L1dtkLeIz-M)

### [A6. Statecharts: 복잡한 UI 상태를 지배하는 방법](https://youtu.be/Hv_PhrfwerQ)
  - [statecharts](https://statecharts.github.io/)
  	- [XState](https://xstate.js.org/)
    
### [B1. React Native에서 Pinch Zoom을 구현하면서 배운 것들](https://youtu.be/ddnr8RXQ9HU)
