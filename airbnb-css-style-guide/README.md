# airbnb-css-style-guide

Airbnb CSS 스타일 가이드 따라하기 (https://github.com/airbnb/css)

## 용어

### Rule declaration

"rule declaration"이란, 여러개의 property가 있는 그룹을 하나의 selector 혹은 여러개의 selector에 결합시키는 행위를 의미한다.

```css
.listing {
  font-size: 10px;
  line-height: 1.2;
}
```

### Selectors

rule declaration에서 "selector"란, 정의된 property들이 DOM tree의 어느 엘리먼트에 적용될지 정하는 문자열을 의미한다. Selector는 HTML, class, ID, 속성 등을 매칭할 수 있다.

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

마지막으로, Properties란 Rule declaration 에서 선택된 엘리먼트에 스타일을 주는 것을 의미한다. Properties는 key-value 쌍으로 이루어져 있고, 하나의 rule declaration 에는 여러개의 property declaration 이 들어갈 수 있다.

```css
/* some selector */
 {
  background: #f1f1f1;
  color: #333;
}
```
