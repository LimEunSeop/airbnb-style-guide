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

## CSS

### Formatting

- 들여쓰기를 soft tabs로 하라. soft tabs 란, 공백이 2개짜리인 탭을 말한다.
- 클래스 이름을 Camel case 로 하지말고 dash 를 사용해서 단어를 구분하자.
  - BEM 방법론을 사용한다면 Underscore와 PascalCase도 괜찮다.
- ID 선택자는 사용하지 말라.
- rule declaration에서 2개 이상의 선택자를 사용할 때, 선택자를은 각각 한 줄을 차지하도록 하자.
- rule declaration 에서 중괄호를 열 때 한칸 공백을 두자.
- 속성을 작성할때 `:` 앞에는 공백이 없고 뒤에는 한칸이 있어야한다.
- 중괄호를 닫을때는 새로운 줄에서 닫는다.
- rule declaration들 사이는 한 줄 공백으로 구분하자.

#### Bad

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}
.no,
.nope,
.not_good {
  // ...
}
#lol-no {
  // ...
}
```

#### Good

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

## Comments

- Sass 를 사용해서 line comments (`//`) 를 자주 사용하도록 하자.
- end-of-line comments 사용하지 말자(코드 뒤에 주석 다는것). 주석은 스스로 한 줄을 차지하도록 해야한다.
- self-documenting이 안되는 코드는 자세한 주석을 사용해야 한다! self-documenting이란, 주석 없이 읽는것 그 자체로 의미를 파악할 수 있는 것을 의미한다.
  - z-index 에 관한 설명
  - 브라우저 특정 해킹 & 트릭을 적용했을 때
