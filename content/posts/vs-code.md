---
title: "Vs Code"
date: 2020-12-23T19:09:09+09:00
draft: false
tags: ["tool", "ide", "vs-code"]
---

# VS-Code의 편리함에 관하여

## 단축키

| 기능 설명 | 단축키 | 비고 |
| :--:|:--:|:--|
| 부분 주석 | Shitf + Alt + a | Ctrl + / 를 넘는 획기적인 기능 |
| 멀티 커서 | Ctrl + Alt + {{ UpArrowKey \| DownArrowKey }} | |
| 멀티 커서 | Shift + Alt + LeftMouseBtn | ver Mouse |
| 그룹 전환 | Ctrl + Alt + {{ LeftArrowKey \| RightArrowKey }} |
| 커서 이동 | Ctrl + Alt + \ | 현재 scope의 양쪽 끝으로 토글 |

## 검색 기능

### 정규표현식
  - 형태
    - 검색 : someString((\d+))
    - 치환 : someString($1)
  - Case 
    - 설명: 공백문자가 있거나 없거나
    - 문법: [\s+]?
    - 예시: function([\s+]?{[\s+]?idx[\s+]?:[\s+]?(\d+)
