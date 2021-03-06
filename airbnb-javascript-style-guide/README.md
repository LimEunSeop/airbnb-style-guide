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

## Arrays

<a name="arrays--1"></a><a name="4.1"></a>

- [4.1](#arrays--1) array 만들때 리터럴 문법을 사용하자. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor)

  ```javascript
  // bad
  const items = new Array()

  // good
  const items = []
  ```

<a name="arrays--2"></a><a name="4.2"></a>

- [4.2](#arrays--2) array에 아이템 삽입시 직접 할당 하지 말고 Array#push 를 사용하자

  ```javascript
  const someStack = []

  // bad
  someStack[someStack.length] = 'abracadabra'

  // good
  someStack.push('abracadabra')
  ```

<a name="arrays--3"></a><a name="4.3"></a>

- [4.3](#arrays--3) array 복사시에는 spread 문법을 필히 사용하자.

  ```javascript
  // bad
  const len = items.length
  const itemsCopy = []
  let i

  for (i = 0; i < len; i += 1) {
    itemsCopy[i] = items[i]
  }

  // good
  const itemsCopy = [...items]
  ```

<a name="arrays--4"></a><a name="4.4"></a>

- [4.4](#arrays--4) **iterable object** 를 array 로 바꿀때는 `Array.from` 보단 spread 문법을 사용하자.

  ```javascript
  const foo = document.querySelectorAll('.foo')

  // good
  const nodes = Array.from(foo)

  // best
  const nodes = [...foo]
  ```

<a name="arrays--5"></a><a name="4.5"></a>

- [4.5](#arrays--5) **array-like 오브젝트**를 array로 바꿀때는 `Array.from`을 사용하자. 그니까 정리하자면, object 인데 속성이 Array 처럼 생겼다! 그때는 `Array.from`, 그 이외의 모든 iterable은 spread 문법 사용하기!! spread 는 iterable 이면 가능하니까!!!!!

  ```javascript
  const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 }

  // bad
  const arr = Array.prototype.slice.call(arrLike)

  // good
  const arr = Array.from(arrLike)
  ```

<a name="arrays--6"></a><a name="4.6"></a>

- [4.6](#arrays--6) iterable을 map 하려면 spread 문법 쓰지말고 `Array.from`을 사용하자!!! spread 쓰면 배열이 새로 생성되니까 비효율적이다!

  ```javascript
  // bad
  const baz = [...foo].map(bar)

  // good
  const baz = Array.from(foo, bar)
  ```

<a name="arrays--7"></a><a name="4.7"></a>

- [4.7](#arrays--7) 배열 메소드 콜백에서 return 문을 꼭 사용하도록 하자. body 가 한줄이고 사이드이펙트를 발생시키지 않는 코드라면 return 생략해도 된다. eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

  ```javascript
  // good
  ;[1, 2, 3].map((x) => {
    const y = x + 1
    return x * y
  })

  // good
  ;[(1, 2, 3)].map((x) => x + 1)

  // bad = no returned value means `acc` becomes undefined after the first iteration
  ;[
    [0, 1],
    [2, 3],
    [4, 5],
  ].reduce((acc, item, index) => {
    const flatten = acc.concat(item)
  })

  // good
  ;[
    [0, 1],
    [2, 3],
    [4, 5],
  ].reduce((acc, item, index) => {
    const flatten = acc.concat(item)
    return flatten
  })

  // bad
  inbox.filter((msg) => {
    const { subject, author } = msg
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee'
    } else {
      return false
    }
  })

  inbox.filter((msg) => {
    const { subject, author } = msg
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee'
    }

    return false
  })
  ```

## Destructuring

<a name="destructuring--1"></a><a name="5.1"></a>

- [5.1](#destructuring--1) 오브젝트의 다수 속성에 접근할 때는 object destructuring을 사용하자. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

  > 그 이유는, destructuring 이 불필요한 객체 참조를 줄여주고 object 에 대한 반복적인 엑세스를 줄여주기 때문이다. 반복적인 object 엑세스는 코드의 중복이 일어나고, 가독성에 좋지 않으며, 실수를 할 여지가 많이 생긴다. destructuring은 또한 코드블락에서 object의 어떤 속성을 사용할 건지 한 군데에서 명확하게 정해주는 역할을 한다. destructuring을 사용하지 않는다면, 코드블락 전체를 읽어가며 object에서 어느 속성을 사용하고 있는지 일일히 확인해야 하는 불편함이 따를것이다..

  ```javascript
  // bad
  function getFullName(user) {
    const firstName = user.fiestName
    const lastName = user.lastName

    return `${firstName} ${lastName}`
  }

  // good
  function getFullName(user) {
    const { firstName, lastName } = user
    return `${firstName} ${lastName}`
  }

  // best
  function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`
  }
  ```

<a name="destructuring--2"></a><a name="5.2"></a>

- [5.2](#destructuring--2) 배열도 destructuring 하자. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

  ```javascript
  const arr = [1, 2, 3, 4]

  // bad
  const first = arr[0]
  const second = arr[1]

  // good
  const [first, second] = arr
  ```

<a name="destructuring--3"></a><a name="5.3"></a>

- [5.3](#destructuring--3) 여러 값을 리턴할때는 array destructuring 말고 object destructuring을 하자.

  > 호출하는 곳의 변경 없이 새로운 속성을 추가하거나 순서를 변경할 수 있기 때문.

  ```javascript
  // bad
  function processInput(input) {
    // then a miracle occurs
    return [left, right, top, bottom]
  }

  // the caller needs to think about the order of return data
  const [left, __, top] = processInput(input)

  // good
  function processInput(input) {
    // then a miracle occurs
    return { left, right, top, bottom }
  }

  // the caller selects only the data they need
  const { left, top } = processInput(input)
  ```

## Strings

<a name="strings--1"></a><a name="6.1"></a>

- [6.1](#strings--1) 문자열을 single quote(`''`)로 표기하자. eslint: [`quotes`](https://eslint.org/docs/rules/quotes)

  ```javascript
  //bad
  // prettier-ignore
  const name = "Catp.Janeway"

  // bad - template literals should contain interploation or newlines
  const name = `Capt. Janeway`

  // good
  const name = 'Capt. Janeway'
  ```

<a name="strings--2"></a><a name="6.2"></a>

- [6.2](#strings--2) 100자 이상의 문자열은 문자열 접합으로 여러줄로 나누면 안된다.

  > 줄이 깨진 문자열은 작업을 어렵게 하고 잘 검색이 안된다.

  ```javascript
  // bad
  const errorMessage =
    'This is a super long error that was thrown because \
  of Batman. When you stop to think about how Batman had anything to do \
  with this, you would get nowhere \
  fast.'

  // bad
  const errorMessage =
    'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.'

  // good
  const errorMessage =
    'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.'
  ```

<a name="strings--3"></a><a name="6.3"></a>

- [6.3](#strings--3) 프로그래밍적으로 문자열 빌드할때는 concatenation 보다는 template strings를 사용하자. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

  > 더 읽기 쉽고, 적절한 줄바꿈과 interploation이 가능한 명료한 문법을 제공한다.

  ```javascript
  // bad
  function sayHi(name) {
    return 'How are you, ' + name + '?'
  }

  // bad
  function sayHi(name) {
    return ['How are you, ', name, '?'].join()
  }

  // bad
  // prettier-ignore
  function sayHi(name) {
    return `How are you, ${ name }?`
  }

  // good
  function sayHi(name) {
    return `How are you, ${name}?`
  }
  ```

<a name="strings--4"></a><a name="6.4"></a>

- [6.4](#strings--4) 문자열에 `eval()` 을 절대 쓰지 말자. 취약점이 매우 많다. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

<a name="strings--5"></a><a name="6.5"></a>

- [6.5](#strings--5) escape 문자를 남발하지 말자. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

  > 백슬래쉬는 정말 필요한 곳에만 써야지, 그렇지 않으면 읽기 불편할 뿐이다.

  ```javascript
  // bad
  // prettier-ignore
  const foo = '\'this\' \i\s \"quoted\"';

  // good
  const foo = '\'this\' is "quoted"'
  const foo = `my name is '${name}'`
  ```

## Functions

<a name="functions--1"></a><a name="7.1"></a>

- [7.1](#functions--1) 함수 선언문을 말고 함수 표현식을 사용할 것. eslint: [`func-style`](https://eslint.org/docs/rules/func-style)

  > 함수 선언문은 호이스팅돼서 가독성이 떨어지고 유지보수성이 나빠진다. 만약에 함수 정의가 너무 길면, 그때는 모듈로 따로 빼야한다. 함수표현식에도 이름을 주도록 하자. Error 콜백에 대한 assumption을 제거해준다.

  ```javascript
  // bad
  function foo() {
    // ...
  }

  // bad
  const foo = function () {
    // ...
  }

  // good
  // lexical name distinguished from the variable-referenced invocation(s)
  const short = function longUniqueMoreDescriptiveLexicalFoo() {
    // ...
  }
  ```

<a name="functions--2"></a><a name="7.2"></a>

- [7.2](#functions--2) IIFE 패턴을 사용하려면 함수표현식으로 만들기 위하여 괄호로 꼭 묶어라. eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife)

  > 함수 선언문은 IIFE 가 안된다. 괄호로 묶어야 표현식으로 바뀌면서 IIFE가 가능해지게 된다. IIFE 패턴을 쓰기 좋은 때는?? 코드 모듈에서 공개하고 싶은것만 공개하고 전역을 오염시키고 싶지 않을때 쓰면 좋을것 같다.

  ```javascript
  // prettier-ignore
  // immediately-invoked function expression (IIFE)
  // outside, inside 옵션이 있다. 현재는 outside 방식에 의한 묶음이고, 디폴트가 outside이다.
  (function () {
    console.log('Welcome to the Internet. Please follow me.')
  }())
  ```
