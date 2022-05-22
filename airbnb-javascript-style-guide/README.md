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

<a name="objects--5"></a><a name="3.5"></a>

- [3.5](#objects--5) 속성값 축약문법을 사용할 때는 속성 선언부 윗쪽에 같이 배치해두자.

  > 이유는, 축약문법을 사용한 속성이 무엇인지 한눈에 파악 가능하기 때문이다.

  ```javascript
  const anakinSkywalker = 'Anakin Skywalker'
  const lukeSkywalker = 'Luke Skywalker'

  // bad
  const obj = {
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
  }

  // good
  const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJediWaliIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
  }
  ```

<a name="objects--6"></a><a name="3.6"></a>

- [3.6](#objects--6) 부적절한 식별자한테만 따옴표 속성을 사용하자. 관련 eslint rule: [`quote-props`](https://eslint.org/docs/rules/quote-props)

  > 그 이유는, 일반적으로 읽기 쉽기 때문이다. 또한, syntax highlighting 에 유리하고, JS 엔진이 최적화하기 더욱 유리해진다.

  ```javascript
  // bad
  const bad = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
  }

  // good
  const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
  }
  ```

<a name="objects--7"></a><a name="3.7"></a>

- [3.7](#objects--7) `hasOwnProperty`, `propertyIsEnumerable`, `isPrototypeOf` 와 같은 `Object.prototype` 메소드는 호출하지 말자. 관련 eslint rule: [`no-prototype-buildins`](https://eslint.org/docs/rules/no-prototype-builtins)

  > 이유는, 해당 메소드들이 다음과 같은 상황으로 가려질 수 있기 때문이다. - `{ hasOwnProperty: false }` 와 같이 새로운 속성으로 덮어지거나 - null object 로 생성될 수도 있다. `Object.create(null)`

  ```javascript
  // bad
  console.log(object.hasOwnProperty(key))

  // good
  console.log(Object.prototype.hasOwnProperty.call(object, key))

  // best
  const has = Object.prototype.hasOwnProperty // 모듈 스코프에서 검색을 캐시한다.
  console.log(has.call(object, key))
  /* or */
  import has from 'has' // https://www.npmjs.com/package/has
  console.log(has(object, key))
  ```

<a name="objects--8"></a><a name="3.8"></a>

- [3.8](#objects--8) 얕은 복사를 할 때는 `Object.assign`보단 spread 문법을 사용하자. 특정 속성이 생략된 새로운 객체를 얻고 싶을 땐 rest parameter 문법을 사용하자. eslint: [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

  ```javascript
  // very bad
  const original = { a: 1, b: 2 }
  const copy = Object.assign(original, { c: 3 }) // 'original'을 mutate해서 좋지않음
  delete copy.a // 얘도 마찬가지ㅇ

  // bad
  const original = { a: 1, b: 2 }
  const copy = Object.assign({}, original, { c: 3 }) // copy => { a: 1, b: 2, c: 3 }

  // good
  const original = { a: 1, b: 2 }
  const copy = { ...original, c: 3 } // copy => { a: 1, b: 2, c: 3 }

  const { a, ...noA } = copy // noA => { b: 2, c: 3 }
  ```
