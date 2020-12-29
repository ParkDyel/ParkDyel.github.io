---
title: "파일명 규칙 바꾸는 스크립트 작성하기!"
date: 2020-12-30T03:53:46+09:00
draft: false
tags: ["Coding"]
---

# 파일명 규칙 바꾸는 스크립트 작성하기!

## 🕐 현재 시각...
새벽 2시. 잠들기엔 아쉽고 그렇다고 공부를 하자니 머리에는 들어오지 않을것 같아 사진을 정리하기로 한다.

사진을 정리하기 위해 폴더를 열어보니, 중간에 규칙명이 바뀐것이 신경쓰이지 않는가? _공부를 못하는 사람들이 꼭 원래 목적을 잊고 다른 길로 간다는데 딱 그 경우이다._ 파일 갯수를 보니 꽤 많아 도저히 수작업으로는 진행할수 없었다. 그래도 나름 규칙성이 있어보여 삽질을 해보기로 한다!

## 🐱‍🏍 목표

이전에 사용했던 규격: {LabelKo}\_{Title}\_{Date}.{Ext} \
현재 사용중인 규격: {LabelEn}\_{Title}\_{Date}.{Ext}

### 🤔 작성하기전 고려한 것

- Title에도 underBar가 있을 수 있다.

### 🔧 코딩

함수는 하나씩 테스트 해보며 작성했다.
코드가 너무 적나라해서 따로 설명은 남기지 않는다.

```javascript
const fs = require("fs")

const isDir = (path) => {
  return new Promise( (resolve, reject ) => {
    try {
      const stat = fs.lstatSync(path);
      if (stat.isDirectory()) {
        resolve(path);
      } else {
        reject(`\"${path}\" is not directory`)
      }
    } catch (e) {
      reject(e);
    }
  })
}

const getListInDir = (path) => {
  return fs.readdirSync(path, { withFileTypes: true })
};

const filterContainTheString = (theString) => (theList) => theList.filter(x => x.includes(theString) )

// const renameFile = (subStr, newSubStr) => (oldPath) => oldPath.replace(subStr, newSubStr); 테스트 코드

const renameFile = (subStr, newSubStr) => async (oldPath) => {
  const newPath = oldPath.replace(subStr, newSubStr);
  await fs.renameSync(oldPath, oldPath.replace(subStr, newSubStr));
  return newPath;
};

if (require.main === module) {
  const thePath = './'
  const theLabel = "진행"
  const willLabel = "on"
  const filterContainTheStringForUser = filterContainTheString(theLabel)
  const renameFileReplaceUnderBarAfterLabel = renameFile(`${theLabel}_`, `${willLabel}-`)
  const renameFileReplaceUnderBarBeforeDate = renameFile(/_(\d+)\./, (match, p1) => `-${p1}.` )

  isDir(thePath)
    .then(getListInDir)
    .then(theList => theList.filter((dirent) => dirent.isFile()))
    .then(theList => theList.map((dirent) => dirent.name))
    .then(filterContainTheStringForUser)
    .then(theList => theList.map(x => renameFileReplaceUnderBarBeforeDate(x)))
    .then(theList => theList.map(x => renameFileReplaceUnderBarAfterLabel(x)))
    .then(x => console.log(x))
    .catch(e => console.log(e))
}
```

### 🤔 개선해야할 것

- Label에 대해 List 처리
  - 바꿔야 할 대상이 한 개의 Label 뿐이라, 정규표현식을 사용하지 않았지만, 바꿔야 할 Label이 여러개라면 정규 표현식과 List를 이용하여 처리할 수 있지 않을까?
- 두 번의 순회
  - 현재 Label 부분과 Date 부분을 나눠서 처리하고 있는데, 정규 표현식을 잘 작성하면 한번에 할 수 있을 것 같다. 성능 차이가 큰 부분이니 개선하면 좋을것 같지만 이미 코드는 실행되었고 파일명이 변경되어 다음 기회에 고려해보도록 한다.

## 😘 뭔가

프로젝트에 넣기는 민망스럽고, 남기기엔 이 밤이 억울해 작성한다.
