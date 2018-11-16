---
layout: post
title: "React Bind"
subtitle: "About React Bind"
background: "/background.jpg"
---

# React Bind

***

### React Bind ?  
React 개발을 하다보면 항상 마주치는게 메소드 바인딩이다.  
아래와 같은 컴포넌트를 만들었다고 가정해보자.  

```javascript
class MyComponent extends Component {
    DoSomething() {
        // ...
    }

    constructor() {
        // ... 

        this.DoSomething = this.DoSomething.bind(this); // (A)
    }
}
```
당연히 우리가 봐야할 구문은 (A)이다.  
"React Example, Sample, 사용법" 등으로 구글링했을 때 샘플 소스의 일부는 저런 형태를 설명하고 있었다.  
하지만 Javascript를 알게 된지 얼마안되어 쉽게 이해할 수 없었고 단순히 사용만 했었다.  
실제로 개발하면서 `bind`를 하지 않아 `undefined` 에러 메시지를 자주 접하게 되었고, 굉장히 반복적인 형태의 코드를 만들어내게 되었다.  
그러다가 알게된 대안 방안이 화살표 함수[^ArrowFunction](Arrow Function)였다.  
자동으로 this를 바인딩 해주기 때문에 그냥 사용하면 된다고 한다.  

```javascript
class MyComponent extends Component {
    DoSomething = () => {
        // ...
    }
}
```
사용하는 것은 매우 편하고 이해하지 않고도 문제는 없다.  
그래도 알고 넘어가자는 생각에, 개발을 하면서 중간 중간 시간을 내서 찾아보게 되었다.  

[^ArrowFunction]: 화살표 함수는 ES6(ECMAScript2015)의 스펙이며, IE에서는 문제가 되니 Transpile, Transpiling, Babel 등 관련 정보를 찾아보길 권장한다.  

***

### Javascript Binding  
Javascript에서는 여러가지 바인딩 방법이 존재한다.  
1. 함수 바인딩  
2. 메소드 바인딩  
3. 객체 생성 시 바인딩(생성자 호출 시 바인딩)  
4. 직접 바인딩(bind, call, apply 함수)   
이러한 방법들에 대해서 아는 범위 내에서 쉽게 설명해보고자 한다.  

***

### 실행 컨텍스트 ?  
바인딩을 설명하기 앞서 우리는 Javascript 실행 컨텍스트라는 것을 알아야 한다.  
실행 컨텍스트(Execution Context)란? Scope, Hoisting, Closure 등 다양한 Javascript의 동작원리를 담고 있는 핵심 원리이다.  
다시 말하자면 실행 컨텍스트는 코드가 실행되기 위한 환경이다.  
실행 컨텍스트는 코드를 객체 형태로 가지게 되는데, 객체의 속성 중 this가 있다.  
this는 기본적으로 전역 객체(window, global 등)를 가리키고 있다가 함수 호출 패턴에 의해 결정되는데, 이것을 바인딩이라고 생각하면 된다.  
즉 "어떤 객체가 this인가?"를 결정하는 것이 바인딩이다.  
중요하고 어려운 내용이므로 자세한 내용은 구글링을 통해 습득하기를 바란다.  
*** 

### 함수 바인딩  
모든 변수는 기본적으로 전역 객체(window, global 등)에 담긴다.  
즉, 웹 브라우저라면 a라는 함수를 선언하면 window.a의 멤버변수/메소드가 된다는 말이다.  

```javascript
var name = "global";

function sayName() {
    var name = "james";
    console.log(this.name); // global
}
console.log(this.name); // global

sayName(); // (A)
window.sayName(); // (B)
```
위 코드에서 함수를 호출하는 부분을 보자.  
위에서 말했듯이 함수는 전역 객체 아래 포함된다.  
즉, `sayName`은 `window` 객체의 메소드이다.  
그러므로 `sayName`의 this는 전역 객체이다.  
***

### 메소드 바인딩  
함수 바인딩을 이해했다면, 메소드 바인딩도 동일하다는 것을 알 수 있을 것이다.  
객체의 메소드는 그 객체가 this에 바인딩 되어 있다.  

```javascript
var name = "global";
var james = {
    name: "james",
    getName: function() {
        return this.name;
    }
}

console.log(james.getName()); // james
``` 
***

### 객체 생성 시 바인딩  
```javascript
var name = "global";
var Person = function(name) {
    this.name = name;
    this.getName =  function() {
        return this.name;
    }
}

var james = new Person("james");

console.log(james.getName()); // james
``` 
***

### 직접 바인딩  
javascript 바인딩을 따르는게 아니라 개발자가 특정 객체에 바인딩 시키는 방법이다.  

```javascript
var Person = function(name){
    this.name = name;
    this.getName =  function() {
        return this.name;
    }
}

var james = {}

console.log(james); // {}

Person.apply(james, ["james"]); // (A)
Person.call(james, "james"); // (B)

console.log(james.getName()); // james
```

(A)와 (B)에서 사용된 apply, call 메소드가 바로 바인딩 메소드이다.  
Object 객체에 있는 메소드기 때문에 모든 객체에서 사용할 수 있다.  

***
