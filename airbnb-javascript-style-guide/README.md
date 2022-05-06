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
