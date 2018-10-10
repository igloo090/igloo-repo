---
type: post
title: "Javascript Clean Code"
category: javascript
---

1. Code Convention : Camel Case
일반적으로 가장 많이 사용되는 코드 스타일이다. 
가장 처음 단어를 제외한 단어들의 첫 문자를 대문자로 표기한다. 
```Javascript 
var currentTime; 
function getUser() {}
```

2. 의미있고 쉽게 그리고 간략하게
변수나 함수 이름을 결정할 때 심플하도록 짓는 것이 좋다.
이름이 길수록 복잡해지고 이해도가 떨어지게 된다. 
단순 명료하게 규칙적이게 짓도록 노력하자. 
```Javascript 
// 모든 의미를 풀어쓰려고 하다가는 끝이 없다...
var userNameFormTableWithFirstName;
// 간략하게 가장 중요한 내용을 이름으로 활용하자.
var userName;
```

3. 공백, 들여쓰기는 필수
(), [], {} 괄호 기호에 맞추어 항상 들여쓰기를 하자.
공백은 구분되어 잘 보여지도록 적절하게 사용한다. 
```Javascript 
// 위, 아래를 보았을 때 아래가 좀 더 명확하게 연산자가 구분된다. 
var isComplete = (currentProgress>100);
var isComplete = (currentProgress > 100);
```

4. 비교 연산자(동등 연산자)
다른 언어를 접해본 프로그래머라면 ==, != 연산자는 익숙할 것이다. 
Javascript에서는 보다 정교한 비교 연산자를 제공하는데 이를 잘 활용하는 것이 중요하다. 
대충 쓰다가는 자동 형변환으로 본인이 의도한 목적대로 비교가 되지 않을 수 있다. 
```Javascript
if('1' === 1) // false
if('1' == 1)  // true (자동 형변환)
```

5. Literal
문자열은 'Apple', "Apple" 처럼 '', "" 기호 둘 다 사용 가능하다. 
하지만 기본적으로 ""기호를 사용하여 묶는 것이 좋다. 
객체 리터럴의 경우 중괄호를 열고 닫히는 들여쓰기가 같아야 한다. 
```javascript
// 멤버 변수나 메소드가 많아지면 한줄로 쓰는 것은 좋지 않다. 
var user = {name: "Tom", age: 20, };
// Method 전에 한줄 공백이 있으면 좋다.
var user = {
    name: "Tom",
    age: 20,

    getName: function() {
        return this.name;
    }
};
``` 

6. 상수, 고정 값
고정되어 있는 값에 대해서는 const 자료형을 사용한다. 
그리고 변수 명은 모두 대문자로 구성하는 것이 좋다. 
```javascript
const TYPE_UNKNOWN = 0;
const TYPE_NORMAL = 1;
const ERROR_MESSAGE = "Error!";
```

