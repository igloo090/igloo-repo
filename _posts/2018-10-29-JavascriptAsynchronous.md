---
layout: post
title: "Javascript Asynchronous"
subtitle: "About Javascript Asynchronous"
background: "/background.jpg"
---

# Javascript Asynchronous  

***

### Synchronous, Asynchronous ?  
동기(Synchronous), 비동기(Asynchronous)를 의미하며 단순한 단어 해석으로는 쉽게 감이오지 않을 수 있다.  
처음 동기, 비동기를 이해하기 위해서는 단순히 "기다린다(동기), 기다리지 않는다(비동기)"로 이해했다.  
프로그래밍은 기본적으로 동기적이다.  
즉, 순차적으로 코드를 실행한다고 보면 된다.  
Javascript에서도 마찬가지로 순차적으로 실행된다.  
```javascript 
console.log('Hello World');
console.log('Every Body!');
// Hello World
// Every Body!
```
그렇다면 비동기는 왜 사용할까?  
단순한 출력이나 처리는 동기적으로 충분히 가능하지만 다소 시간이 걸리는 작업들은 순차적으로 실행하기는 어렵다.  
특히나 통신, 파일 I/O 등 많은 시간이 필요한 작업은 대부분의 개발자는 비동기로 처리할 것이다.  
그렇다면 Javascript에서는 비동기를 어떤 형태로 처리할까?  

***

### Callback  
Callback은 원하는 함수를 호출(A)할 때 "내가 만든 코드(Function)를 함수 인자"로 넘긴다.  
이 인자를 Callback 함수라고 말하며 호출한 함수(A)가 처리된 후 Callback 함수를 호출하는 것을 Callback이라고 이해하면 된다.  
다른 언어에서는 옵저버 패턴(Observer Pattern), 리스너 패턴(Listener Pattern)이라고 불리는 방법도 콜백으로부터 시작된다.  

Javascript에서는 Callback으로 비동기를 지원하며, 정말 자주 사용되므로 반드시 알고 넘어가야 한다.  
그렇다면 실제 소스코드에서는 어떻게 표현될까?
```Javascript
console.log('I');

setTimeout(
    function () { 
        console.log('Am'); 
    }, 
    3000
);

console.log('Groot');
// I Groot Am
```
소스코드를 보았을 땐 왠지 "I Am Groot"라고 출력되어야 할 것 같지만, 실제로는 "I Groot Am"라고 출력된다.  
이는 setTimeout이라는 함수를 통해 Callback 함수로 이름없는 함수[^익명함수]를 전달하며 함수는 "Am"을 출력한다.  
이름없는 함수는 3초(코드 상 3000밀리초) 후 실행되게 된다.  
쉽게 말하자면, 순차적(동기)으로 "I" 출력, setTimeout 호출, "Groot" 출력, "Am" 출력 순으로 처리된다.  

위 샘플코드에서는 비동기 처리가 무의미해보이지만 실제 현업에서는 다수의 소스코드가 비동기 형태로 처리된다는 것을 명심해야 한다.  

[^익명함수]: 이름없는 함수로 불린다. 함수의 구현부만 존재하고 함수의 이름은 없다. 즉, 구현부가 존재하는 위치(보통 함수의 인자)에서 바로 사용되고 버려지는 함수이다. 

***

### Callback Hell
콜백 지옥(Callback Hell), Javascript 관련 자료를 찾다보면 콜백 지옥이라는 말을 들어볼 수 있다.  
보통 웹 서비스를 개발하다 보면 쉽게 생각하거나 접할 수 있는 문제이다.  
콜백을 여러번에 걸쳐 호출하다 보면 과연 결과는 잘 처리 될까? 하나의 함수라도 실패 혹은 에러가 발생한다면 추적이 쉬울까? 소스코드의 가독성은 괜찮은가? 와 같은 여러가지 의문점들이 들기 시작한다.  

그렇다면 이 콜백 지옥을 해결하는 방법은 무엇이 있을까?

***

### Promise  
Promise는 비동기 처리에 사용되는 객체로 ES6부터 사용할 수 있다.  
Promise 객체를 생성할 때 인자로 함수를 주고, 함수에서는 비동기 처리 후 결과에 따라 Resolve 혹은 Reject 처리한다.  
Promise는 3가지 상태를 가진다.  
1. Pending(대기)  
: 비동기 처리가 완료되지 않은 상태.  
2. Fulfilled(이행)  
: 비동기 처리가 완료되어 결과 값을 반환한 상태.  
3. Rejected(실패)  
: 비동기 처리가 실패하거나 오류가 발생한 상태.  

```javascript
// Pending
var p = new Promise(
    function(resolve, reject)
    {
        // Fulfilled
        resolve(res);

        // Rejected
        reject(res)
    }
);

p()
// 성공(이행)에 따른 처리
.then(function() { ... })
// 실패에 따른 처리
.catch(function() { ... });
```

***

### Async/Await  
ES8부터 사용할 수 있는 문법으로 브라우저 지원 범위를 잘 따지고 Babel을 통해 ES5로 Transpile 후 사용할 수 있다.  
내용은 추후 다른 포스트로 작성할 예정이다.  

***
