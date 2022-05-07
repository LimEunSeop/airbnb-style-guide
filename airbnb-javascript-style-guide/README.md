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
