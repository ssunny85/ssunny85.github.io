---
title:  "Rendering"
excerpt: "브라우저가 렌더링하는 방법 설명글입니다."
date: 2020.01.31
tags:
  - browser
  - rendering
---

html, css, javascript 문서를 통해 브라우저에 내용을 그려내는것을 말합니다.

## 렌더링 순서

1. **DOM/CSSOM 형성**

   브라우저는 서버에서 보내준 html과 css, javascript를 받아 html은 DOM(Document Object Model)트리 구조를 형성하고 css는 CSSOM(CSS Object Model) 트리 구조 형성 
   (*여기서 DOM과 CSSOM은 독립적인 객체 트리 구조)*

2. **Render Tree 생성**

   DOM에 스타일 정보를 설정(CSSOM)을 더해주면서 Render Tree를 생성 
   (*Render Tree는 브라우저에서 보여줄 내용으로만 구성된다. 예를 들어 스타일 속성으로 display:none 설정된 노드는 포함되지 않는다.*)

3. **Layout**

   디바이스의 viewport에 따라 Render Tree 노드들이 가지고 있는 크기, 위치를 계산하는 단계

4. **Paint**

   Layout 단계가 완료되면 Layer로 구분해서 실제 보여줄 속성대로 계산하는 단계. 텍스트, 컬러, 배경, 그림자 등 효과 처리 

5. **Composite**

   Paint 단계에서 Layer로 나눠진것들을 실제 화면에서 보는것 처럼 합쳐주는 단계


## Reflow/Repaint

초기 렌더링이 된 이후 이벤트 또는 애니메이션으로 인해 스타일 또는 노드가 변경 되었을 경우 아래 흐름으로 실행.
  `JavaScript 실행 → Style 변경 → Layout → Paint → Composite`

### Reflow

   Layout에 영향을 주는 style의 크기, 위치 또는 노드 추가/삭제 변경인 경우 다시 계산해서 다시 Layout - Paint 단계를 거치는 것.

* Reflow를 일으키는 css 속성:
   width, height, position, top, left, bottom, right, margin, padding, border, float 등

### Repaint

   Layout에 영향을 미치지 않는 배경 컬러, 폰트 컬러 등의 변경인 경우 Layout 단계를 거치지 않고 Paint 단계만 다시 실행.

* Repaint만 일으키는 css 속성:
   background, color, visibility 등

### Reflow/Repaint에 영향을 주지 않는 속성
   transform, opacity, cursor, orphans, perspective 등

[CSS Triggers 참고 URL: https://csstriggers.com/](https://csstriggers.com/){: .text-link target="_blank"}

* 예)
  하나의 Object 위치 변경 애니메이션을 만드는 경우 Layout 에 영향을 주는 position 속성을 이용하는 것보다 transform 속성을 이용하는 것이 더 자연스러운 효과를 줄 수 있다.
