# 08. 이넘

## 8.0. 출처

- 캡틴판교, 『쉽게 시작하는 타입스크립트』, 길벗(2023)

<br>

## 8.1. 이넘(enum)이란?

- 자바스크립트에는 없지만 타입스크립트에서는 지원함
- **특정 값의 집합을 의미하는 데이터 타입**
- 상수 집합

```javascript
function getDinnerPrice() {
  return 10000 + 2000;
}
```

- `getDinnerPrice()` 함수는 저녁 식사 값을 계산하는 함수
- 코드만 봐서는 10000원과 2000원이 각각 무슨 메뉴를 의미하는지 알 수 없음

```javascript
function getDinnerPrice() {
  const RICE = 10000;
  const COKE = 2000;
  return RICE + COKE;
}
```

- 상수를 사용하여 각 숫자 값에 의미 부여 가능
- **상수**: 변하지 않는 고정 값
- 상수는 이 값이 어떤 의미를 갖는지 알려 줌으로써 가독성을 높이는 장점 있음
- 상수는 보통 모두 대문자로 작성해서 일반 변수와 구분함

<br>

- 이넘: 여러 개의 상수를 하나의 단위로 묶은 것
- 이넘의 역할: 비슷한 성격이나 같은 범주에 있는 상수를 하나로 묶어 더 큰 단위의 상수로 만드는 것

```typescript
enum ShoesBrand {
  Nike,
  Adidas,
  NewBalance,
}

var myShoes = ShoesBrand.Nike;
var yourShoes = ShoesBrand.NewBalance;
```

- 객체의 속성에 접근하듯이 이넘의 이름을 쓰고 `.` 접근자를 이용하여 속성 이름을 붙임

<br><br>

## 8.2. 숫자형 이넘

- 이넘에 선언된 속성은 기본적으로 숫자 값을 가짐

```typescript
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
  Right, // 3
}

console.log(Direction.Up); // 0
```

- 속성 값이 숫자로 지정되는 이유는 타입스크립트의 내부 규칙 때문

```javascript
"use strict";
var Direction;
(function (Direction) {
  Direction[(Direction["Up"] = 0)] = "Up";
  Direction[(Direction["Down"] = 1)] = "Down";
  Direction[(Direction["Left"] = 2)] = "Left";
  Direction[(Direction["Right"] = 3)] = "Right";
})(Direction || (Direction = {}));
```

- 타입스크립트로 작성된 이넘 코드를 자바스크립트 코드로 변환한 결과

```javascript
Direction["Up"] = 0;
```

- 이넘 속성 값으로 숫자가 할당된 부분
- 변수 `Direction`의 `UP` 속성에 0을 할당했기 때문에 `Direction` 객체의 `UP` 속성에 접근하는 형태의 `Direction.Up`을 입력하면 0이라는 결과 나옴

```javascript
// 이 코드는 아래와 같이 동작함
Direction[(Direction["Up"] = 0)] = "Up";

Direction[0] = "Up";
```

- [] 안에서 객체의 속성에 0을 할당하는 코드가 있었는데, 자바스크립트의 동작 방식에 따라 할당 연산자 `=`의 할당 값인 `0`만 남기 때문

```javascript
// `Direction` 변수는 이렇게 정의된 꼴임
Direction.Up = 0;
Direction[0] = "Up";

console.log(Direction.Up); // 0
console.log(Direction[0]); // "Up"
```

- **리버스 매핑(reverse mapping)**: 이넘의 속성과 값이 거꾸로 연결되어 할당되는 것
- 타입스크립트의 이넘에 선언된 속성은 기본적으로 숫자 값을 가짐

<br>

```typescript
enum Direction {
  Up = 10,
  Down, // 11
  Left, // 12
  Right, // 13
}
```

- 속성의 초기값을 변경하는 방법
- 첫 번째 속성의 시작 값을 변경하더라도 순서대로 선언된 이넘 속성의 갑은 1씩 증가하는 규칙 있음

```typescript
enum Direction {
  Up = 10,
  Down = 11,
  Left = 12,
  Right = 13,
}
```

- 명시적으로 값 설정하는 것이 직관적

<br><br>

## 8.3. 문자형 이넘

- 이넘의 속성 값에 문자열을 연결한 이넘
- 모든 속성 값을 다 문자열로 지정해 주어야 하고, 선언된 속성 순서대로 값이 증가하는 규칙 없음

```typescript
enum Direction {
  Up = "Up",
  Down = "Down",
  Left = "Left",
  Right = "Right",
}

console.log(Direction.Up); // "Up"
```

- `Direction` 이넘은 상하좌우 네 방향에 해당하는 속성 값을 가짐
- 문자열로 관리되는 것이 더 명시적

```typescript
enum Direction {
  UP = "UP",
  DOWN = "DOWN",
  LEFT = "LEFT",
  RIGHT = "RIGHT",
}

enum ArrowKey {
  KEY_UP = "KEY_UP",
  KEY_DOWN = "KEY_DOWN",
}
```

- 실무에서 이넘 값을 문자열로 관리하는 사례 더 많음
- 속성 이름과 값을 동일하게 문자열로 관리하는 것도 일반적인 코딩 규칙
- 모두 대문자로 작성하거나 언더스코어(`_`) 사용해도 상관 X

<br><br>

## 8.4. 알아 두면 좋은 이넘의 특징

### 8.4.1. 혼합 이넘

```typescript
enum Answer {
  Yes = "Yes",
  No = 1,
}
```

- 숫자와 문자열을 섞어서 선언 가능
- 하지만 이넘 값은 일괄되게 숫자나 문자열 둘 중 하나의 데이터 타입으로 관리하는 것이 좋음

<br>

### 8.4.2. 다양한 이넘 속성 값 정의 방식

```typescript
enum Authorization {
  User, // 0
  Admin, // 1
  SuperAdmin = User + Admin, // 1
  God = "abc".length, // 3
}
```

- 이넘의 속성 값은 고정 값뿐만 아니라 다양한 형태로 값 할당 가능
- 먼저 선언되어 있는 이넘의 속성 활용 가능
- 덧셈 연산자를 사용하여 계산한 값을 속성 값으로 할당 가능
- 이넘 속성 값을 할당할 때 연산자 등을 활용할 수 있지만 활용도 높지 않음

<br>

### 8.4.3. const 이넘

- 이넘을 선언할 때 앞에 `const`를 붙인 이넘

```typescript
const enum logLevel {
  Debug = "Debug",
  Info = "Info",
  Error = "Error",
}
```

- `const`
  - 변수를 선언할 때 사용하는 예약어
  - 이넘 타입을 정의할 때도 사용 가능
- `const`를 이넘 앞에 붙인 이유는 **컴파일 결과물의 코드양을 줄이기 위함**

```typescript
enum logLevel {
  Debug = "Debug",
  Info = "Info",
  Error = "Error",
}
```

```javascript
// 타입스크립트 컴파일 결과
"use strict";
var logLevel;
(function (logLevel) {
  logLevel["Debug"] = "Debug";
  logLevel["Info"] = "Info";
  logLevel["Error"] = "Error";
})(logLevel || (logLevel = {}));
```

- `logLevel` 이넘을 코드에서 활용하려면 `logLevel`이라는 객체를 내부적으로 선언해서 이넘 속성 값들을 연결해 줘야 함
- 이넘 코드는 컴파일될 때 객체가 이넘의 속성 이름과 값을 연결해 주는 객체를 생성한다는 사실 알 수 있음

```typescript
const enum logLevel {
  Debug = "Debug",
  Info = "Info",
  Error = "Error",
}

var appLevel = logLevel.Error;
```

```javascript
// 타입스크립트 컴파일 결과
"use strict";
var appLevel = "Error"; /* logLevel.Error*/
```

- `const` 이넘은 객체를 생성하지 않고 이넘이 사용되는 곳에서 속성 값을 바로 연결해줌
- 일반 이넘을 변환했을 때 객체 코드가 생성되지 않고 `appLevel` 변수가 바로 `Error` 문자열 값이 할당되는 것을 볼 수 있음
- `const` 이넘은 항상 속성에 고정 값만 넣어 줘야 함
