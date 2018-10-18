---
layout: post
title: "Javascript Module"
subtitle: "About Javascript Module"
background: "/background.jpg"
---

# Javascript Module

***

### Module
순수 Javascript에서는 모듈(Module)이라는 개념을 지원하지는 않지만, Javascript가 구동되는 환경에 따라 모듈화 방법을 제공하고 있다.  
모듈을 만드는 방법은 즉시 실행 함수 표현식과 노출식 모듈 패턴이 있다.  
일반적으로 모듈 혹은 라이브러리라고 말하는 방식은 후자를 말하며, 여러가지 문법이 존재한다.  
ES5에서는 전역 변수 형태로 모듈을 만들며, ES6에서는 export로 모듈을 만든다.  
더 자세한 내용은 아래에서 다루도록 한다.  

* 모듈화의 장점  
모듈화는 자주 사용되는 코드의 재사용성을 증가시키고, 필요한 코드만 로드하여 메모리 낭비를 줄일 수 있고, 웹 브라우저에서는 한번 다운로드된 모듈은 다시 다운로드하지 않고 재사용하기 때문에 트래픽과 로딩시간을 줄일 수 있다.  
이와 같이 여러가지 장점으로 인해 모듈화는 프로그래밍에서 아주 중요한 기술이라고 말할 수 있다.  

* ES5 Module  
ES5에서의 모듈은 windows 객체의 멤버 객체이다.  즉, HTML에서 서로 다른 Javscript를 로드하여도 결국 windows 객체 내에서 동작하기 때문에 제약사항이 생기게 된다.  
가장 대표적인 문제는 서로다른 Javascript 파일에 정의된 같은 이름의 변수는 Scope에 대한 문제가 발생할 여지를 만든다.  
Require, Import 등을 사용하여 이러한 문제를 해결할 수 있다. 

***

### Require
[CommonJS](http://www.commonjs.org/) 포맷으로 Node.js에서 사용되고 있는 모듈화 방식이다.  
require, module.export 문법을 사용하여 모듈을 정의하고 의존성을 만들어낸다.  
```javascript
var student = function() { ... };
module.exports = student;

var student = require('student.js');
```
그렇다면 모듈을 Require 할 때 생성되는 인스턴스는 같은 모듈을 여러번 Require하면 어떻게 될까?  
Node.js [Require 문서](https://nodejs.org/api/globals.html#globals_require)에서 설명은 아래와 같다.  
"Modules are cached in this object when they are required. "  
모듈은 로드 되었을 때 캐시된다.  
캐시된 모듈 인스턴스는 삭제되지 않는 이상 재사용되며, 삭제되었을 경우 다시 재로딩하는 과정을 거치게 된다.  
이러한 캐싱 과정에서 모듈을 구분하기 위해 key 값으로 파일 경로를 사용합니다.  
Windows 또는 일부 다른 OS들도 파일 시스템에서 대소문자를 가리지 않는 경우가 있다.  
이러한 경우 **Node.js에서는 다른 파일로 인식하지만 OS에서는 같은 파일로 인식**될 수 있으므로 주의해야 한다.  

***

### Import
ES6에서부터 지원하는 Javascript 내장된 모듈 포맷이다.  
모듈을 만들기 위해서는 export 토큰을 사용한다.  
```javascript
export function student() { ... };
export default function teacher() { ... };

import { studnet } from '...';
import teacher from '...';
```

***

### Module Loader vs Bundler
* Module Loader  
Runtime에 필요한 모듈을 가져와 사용하는 방식이다.  
* Bundler  
Build 시점에서 모듈들의 의존성 관계를 판단하고 모듈들을 하나의 번들로 만들어낸다.  
브라우저는 번들러가 만들어낸 하나의 모듈만 로드하여 실행하게 된다.  

***

### 찾아보기
RequireJS, SystemJS, Browserify, Webpack

***



