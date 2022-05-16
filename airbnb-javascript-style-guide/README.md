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

<a name="references--1"></a><a name="2.1"></a>

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

<a name="references--2"></a><a name="2.2"></a>

- [2.2](#references--2) 참조를 재할당하고 싶으면, `var` 말고 `let` 을 사용하라. 관련 eslint rule: [no-var](https://eslint.org/docs/rules/no-var)

  > 그 이유는 `var`는 함수 스코프이고 `let` 은 블락 스코프이기 때문이다.

  ```javascript
  // bad
  var count = 1
  if (true) {
    count += 1
  }

  // good, use the let.
  let count = 1
  if (true) {
    count += 1
  }
  ```

<a name="references--3"></a><a name="2.3"></a>

- [2.3](#references--3) `let` 과 `const` 는 블락스코프이고, `var` 는 함수 스코프임을 명심하자.

  ```javascript
  // const와 let은 정의된 블락 안에서만 존재한다.
  {
    let a = 1
    const b = 1
    var c = 1
  }
  console.log(a) // ReferenceError
  console.log(b) // ReferenceError
  console.log(c) // Prints 1
  ```

  `a`, `b` 는 블락 스코프라서 블락 바깥에서 참조하려고 하면 존재하지도 않는 변수를 참조할때 발생하는 ReferenceError가 나고, `c` 는 자신이 속하는 함수가 스코프이므로 블락 바깥에서도 정상적으로 참조가 가능하다.

## Objects

<a name="objects--1"></a><a name="3.1"></a>

- [3.1](#objects--1) object 를 생성할 때 리터럴 문법을 사용하라. 관련 eslint rule: [`no-new-object`](https://eslint.org/docs/rules/no-new-object)

  ```javascript
  // bad
  const item = new Object()

  // good
  const item = {}
  ```

<a name="objects--2"></a><a name="3.2"></a>

- [3.2](#objects--2) 객체 생성시 객체명을 동적으로 만들고 싶을 때 computed property를 사용하자.

  > 속성을 한군데에 보기좋게 모두 정의하기 위함이다.

  ```javascript
  function getKey(k) {
    return `a key names ${k}`
  }

  // bad
  const obj = {
    id: 5,
    name: 'San Francisco',
  }
  obj[getKey('enabled')] = true

  // good
  const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey('enabled')]: true,
  }
  ```

<a name="objects--3"></a><a name="3.3"></a>

- [3.3](#objects--3) 오브젝트 메서드 축약문법을 사용하자. 관련 eslint rule: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand)

  ```javascript
  // bad
  const atom = {
    value: 1,

    addValue: function (value) {
      return atom.value + value
    },
  }

  // good
  const atom = {
    value: 1,

    addValue(value) {
      return atom.value + value
    },
  }
  ```

<a name="objects--4"></a><a name="3.4"></a>

- [3.4](#objects--4) 속성값도 축약문법을 사용하자. 관련 eslint rule: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand)

  > 그 이유는? 더 짧고, 설명에 유리하기 때문

  ```javascript
  const lukeSkywalker = 'Luke Skywalker'

  // bad
  const obj = {
    lukeSkywalker: lukeSkywalker,
  }

  // good
  const obj = {
    lukeSkywalker,
  }
  ```
