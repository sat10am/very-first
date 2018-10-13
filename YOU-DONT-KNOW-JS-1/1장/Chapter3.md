
# 3.1 구문

객체는 다음 두 가지로 정의한다

- 선언적 형식( **Declarative** / **Literal** )
```javascript
// 한번의 선언으로 다수의 프로퍼티 추가 가능
var myOjb = {
    key1 : value1,
    key2 : value2
}
```
- 생성자 형식 (매우 드물게 사용)
```javascript
// 프로퍼티를 하나하나 추가해야 함
  var myObj = new Object();
  myObj.key = value;
```
---

# 3.2 타입

7가지 JS 주요 내장 타입 (language types)

**기본 자료형 (Primitive Data Type)**

- null
- undefined
- boolean
- number
- string
- symbol (ES6)

**객체형 (Object Type)**

- object
```javascript
// null type이 object로 나오는 것은 언어 자체 버그이다
typeof null
"object"
```
---

## **Complex Primitive**

자바스크립트의 모든 것이 객체다?

→   Complex Primitive라는 특별한 하위 타입들이 존재

- **함수 Function**

  > Function is a sub-type of object (technically, a `callable object`).

      function name()
      {
      	return "godori"
      };

      var obj = {};

  [Javascript Tutorial | Functions, First Class Citizens or Callable Objects | Ep18](https://www.youtube.com/watch?v=rf7zr3rGBGU)

  : Callable Object 로써의 Fuction에 관하여 참고할만한 영상

  > Functions in JS are said to be `first class` in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

  - 인자로 전달 할 수 있다.

  - 다른 함수로부터 반환되는 값으로 사용할 수 있다.

  - 변수나 자료 구조에 할당할 수 있다.

  - 동적으로 프로퍼티 할당이 가능하다.

- **배열 Array**

  -  좀 더 구조적인 객체의 일종

![](https://yuml.me/b2af19c6.png)

---

## **내장 객체 Built-in Objects**

생김새 때문에 마치 클래스처럼 느껴지지만 이들은 내장 함수일 뿐이다.

- `String`
- `Number`
- `Boolean`

- `Object`
- `Function`
- `Array`
- `RegExp`

- `Date`

- `Error`

각각 생성자로 사용되어 하위 타입의 새 객체를 생성한다.
```javascript
    var str = "그냥 문자열";
    typeof str;                                // "string"
    str instanceof String;                     // false

    var strObj = new String("객체 문자열");
    typeof strObj;                             // "object"
    strObj instanceof String                   // true

    // 객체 하위 타입 확인
    Object.prototype.toString.call( strObj );  // [object String]
```

- Primitive Literal 로 선언한 string 값은 불변값이므로 원칙적으로 변경이 불가능하다. `(ex. var str = "hello")`
- 문자 갯수를 세거나 문자별로 접근하려면 String 객체가 필요할 것 같지만..
- 자바스크립트는 공짜로 박싱을 해줍니다! (객체로 자동 강제변환)
- 사실 객체를 생성할 일이 거의 없으며, JS 커뮤니티에서도 생성자보다 리터럴 형식을 권장

```javascript
    // 원시 값에서 객체로 강제변환되어 length등의 메소드를 사용할 수 있다.
    var strPrimitive = "그냥 문자열임!"

    console.log( strPrimitive.length );      // 8
    console.log( strPrimitive.charAt(3) );   // "문"
```

기타 내장 객체들의 특징

- `null` ,  `undefined` : 그 자체로 유일하며, 객체 래퍼가 없다.
- `Date` : 리터럴 형식이 없어서 반드시 new로 생성해야 한다!
- `Object`, `Array`,  `Function`, `RegExps` : 리터럴/생성자 무관하게 객체이다.
- `Error` : 예외가 던져질 때 알아서 생성되므로 명시적으론 거의 쓰지 않음

---

# 3.3 내용

## 속성 기술자 (Property Descriptor)

객체의 프로퍼티는 값(value) 말고도 고유한 속성 값들을 가지며, 이는 속성 기술자를 통해 조작할 수 있다.

[Object.defineProperty()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 내장 메소드를 사용하면 속성 기술자 값을 설정할 수 있다.

객체를 생성하면서 속성의 값을 설정하면 **`configurable`**, **`enumerable`**, **`writable`** 의 기본값은 `true` 상태이지만, `defineProperty` 로 직접 값을 입력한 경우 속성 기술자의 기본값은 모두 `false`이다.

속성 기술자의 종류는 다음과 같다.

- **value**

  속성 기술자에 저장된 값이다.(default : `undefined`)

- **configurable**

  이 속성 기술자는 해당 객체로부터 그 속성을 제거할 수 있는지를 기술한다. (default : `false`)

- **enumerable**

  해당 객체의 키가 열거 가능한지를 기술한다. (default : `false`)

- **writable**

  할당연산자를 통해 값을 바꿀 수 있는지를 기술한다. (default : `false`)
