# 이번주 JS로 알고리즘 풀면서 배운 내용 요약

## 1. 에라토스테네스의 체

### 1.1. 설명

![에라토스테네스의 체](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

- 소수를 찾는 방법으로 고대 수학자 에라토스테네스가 발견함
- 알고리즘
	
    - 2부터 소수를 구하고자 하는 구간의 모든 수를 나열
    - 2는 소수이므로 오른쪽에 2를 작성
    - 자기 자신을 제외한 2의 배수를 모두 지우기
    - 남아있는 수 가운데 3은 소수이므로 오른쪽에 3 작성
    - 자기 자신을 제외한 3의 배수 모두 지우기
    - 남아있는 수 가운데 5는 소수이므로 오른쪽에 5 작성
    - 자기자신을 제외한 5의 배수 모두 지우기
    - ...
 
 <br>
 
 - **num까지의 수에서 2부터 num의 제곱근까지 반복하면서 해당 수의 배수를 지우고 남는 수를 구하기**

### 1.2. 적용 문제

[[프로그래머스] 소수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/12921)

```javascript
function solution(n) {
  // index 0이 존재하므로 배열을 n+1로 만들기
  let arr = Array(n + 1).fill(true);

  // 배열의 index 0과 1은 소수가 아니므로 false로 만들기
  arr[0] = false;
  arr[1] = false;

  for (let i = 2; i * i <= n; i++) {
    // 제곱근까지 반복
    if (arr[i]) {
      for (let j = i * i; j <= n; j += i) {
        // 반복문을 i*i부터 시작하는 것은 그 이전의 값은 j 이전의 수에서 이미 확인했기 때문
        arr[j] = false; // 배수 이므로 소수가 아닌 것으로 만듦
      }
    }
  }
  // filter로 arr 중 true인 것만 개수 구하기
  return arr.filter((el) => el).length;
}
```

<br>

## 2. padStart(), padEnd()

ES2017부터 문자열에 `padStart()`와 `padEnd()` 메서드가 표준으로 제공된다.
다양한 용도로 활용할 수 있다는 장점이 있지만 구버전 웹브라우저에서는 호환성 문제가 있다는 단점이 있다.

### 2.1. padStart(자릿수, 채울문자)

- 현재 문자열의 시작을 다른 문자열로 채워, 주어진 길이를 만족하는 새로운 문자열을 반환
- 채워넣기는 대상 문자열의 시작(좌측)부터 적용
- 자릿수가 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환
- 채울문자가 너무 길어서 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 채움
- 채울문자를 쓰지 않으면 기본값인 `""`으로 채워짐

```javascript
'abc'.padStart(10);         // "       abc"
'abc'.padStart(10, "foo");  // "foofoofabc"
'abc'.padStart(6,"123465"); // "123abc"
'abc'.padStart(8, "0");     // "00000abc"
'abc'.padStart(1);          // "abc"
```

### 2.2. padEnd(자릿수, 채울문자)

- 현재 문자열에 다른 문자열을 채워, 주어진 길이를 만족하는 새로운 문자열을 반환
- 채워넣기는 대상 문자열의 끝(우측)부터 적용
- 자릿수가 현재 문자열의 길이보다 작다면 채워넣지 않고 그대로 반환
- 자릿수가 너무 길어 목표 문자열 길이를 초과한다면 좌측 일부를 잘라서 넣음
- 채울문자를 쓰지 않으면 기본값인 `""`으로 채워짐


```javascript
const str1 = 'Breaded Mushrooms';
console.log(str1.padEnd(25, '.'));
// Expected output: "Breaded Mushrooms........"

const str2 = '200';
console.log(str2.padEnd(5));
// Expected output: "200  "
```
