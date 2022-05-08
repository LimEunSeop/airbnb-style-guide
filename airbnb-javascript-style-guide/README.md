# aribnb-javascript-style-guide

Airbnb 자바스크립트 스타일 가이드 따라하기 (https://github.com/airbnb/javascript)

## Types

<a name="types--primitives"></a><a name="1.1"></a>

- [1.1](#types--primitives) **Primitives**: 원시타입은 값 그 자체에 동작한다.

  - `string`
  - `number`
  - `boolean`
  - `null`
  - `undefined`
  - `symbol`
  - `bigint`

  ```javascript
  const foo = 1
  let bar = foo

  bar = 9

  console.log(foo, bar) // => 1, 9
  ```

  - Symbol 과 BigInt 타입은 제대로 polyfill 이 안된다. 따라서 native 하게 지원하지 않는 환경이라면 사용하지 않는것이 좋다.

<a name="types--complex"></a><a name="1.2"></a>

- [1.2](#types--complex) **Complex**: complex 타입에 접근하면, 값 그 자체가 아닌 그 값이 참조하는 곳에 동작한다.

  - `object`
  - `array`
  - `function`

  ```javascript
  const foo = [1, 2]
  const bar = foo

  bar[0] = 9
  console.log(foo[0], bar[0]) // -> 9, 9
  ```

## References

<a name="references--1"></a><a name="2-1"></a>

- [2.1](#references--1) `var` 사용을 피하고 웬만한 참조를 `const` 를 사용해서 하자. 관련 eslint rule: [`prefer-const`](https://eslint.org/docs/rules/prefer-const), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign)

  > 이렇게 하면 참조가 바뀔일이 없어서, 버그가 생길 일도 없고 코드가 어려워질 일도 없으진다.

  ```javascript
  // bad
  var a = 1
  var b = 2

  // good
  const a = 1
  const b = 2
  ```
