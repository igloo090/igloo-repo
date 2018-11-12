---
layout: post
title: "Javascript Array Method"
subtitle: "About Javascript Array Method"
background: "/background.jpg"
---

# Javascript Array Method  
Javascript에서 제공하는 배열(Array) 메소드에 대해 설명해보고자 한다.  
굉장히 자주 사용되며, 유용한 메소드이고 소스 분석에서도 꼭 필요하므로 알고 넘어가도록 하자.  

***

### indexOf  
`indefOf` 메소드는 배열에서 지정된 요소를 찾고 첫번째 인덱스를 반환하거나 찾지 못할 경우 -1을 반환한다.  
일반적으로 배열에서 특정 값이 존재 여부를 체크하기 위해서 많이 사용한다.  

```javascript
var a = [2, 9, 9]; 
a.indexOf(2); // 0 
a.indexOf(7); // -1

if(a.indexOf(7) === -1) {
  // 요소가 배열에 존재하지 않습니다.
}
```
`indefOf` 메소드의 반환 값을 비교할 경우 엄격한 비교 연산자(`===, !===`)를 사용하도록 하자.  
[동치 비교 및 동일성](https://developer.mozilla.org/ko/docs/Web/JavaScript/Equality_comparisons_and_sameness)에 대해서는 링크를 통해 알아보도록 한다.  

***

### filter  
`filter` 메소드는 배열에 각 요소들을 테스트하고 그 결과 통과된 요소들을 가진 새로운 배열을 반환한다.  

```javascript 
var numbers = [1, 2, 3, 4, 5];

const result = numbers.filter(number => number > 3);

console.log(result);
// [4, 5]
```

***

### forEach  
`forEach` 메소드는 배열 요소들마다 한번씩 함수를 실행한다.  

```javascript
var numbers = [1, 2, 3];

numbers.forEach(function(element) {
  console.log(element);
});

// output : 1
// output : 2
// output : 3
```

***

### reduce  
`reduce` 메소드는 배열의 가장 왼족 요소부터 오른쪽으로 이동하며 각 요소마다 누적 값과 함께 함수를 호출하여 하나의 값으로 만든다.  

```javascript
var numbers = [1, 2, 3];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

const result = numbers.reduce(reducer);
const result2 = numbers.reduce(reducer, 4);

console.log(result);
// 6

console.log(result2);
// 10
```

***

### map  
`map` 메소드는 배열 내의 모든 요소에 대해 함수를 호출하고 그 결과를 모아 새로운 배열을 반환한다.  
```javascript
var numbers = [1, 2, 3];

const result = numbers.map(x => x * 2);

console.log(result);
// [2, 4, 6]
```

***
