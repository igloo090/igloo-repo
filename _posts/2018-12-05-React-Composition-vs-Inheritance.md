---
layout: post
title: "React Composition vs Inheritance"
subtitle: "About React Composition vs Inheritance"
background: "/background.jpg"
---

# React Composition vs Inheritance

***

## 배경지식  
Javascript, React

***

## Composition vs Inheritance  
React Documents [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html) 문서를 기준으로 이해한 내용을 정리하였다.  

React는 파워풀한 구조의 모델을 가지고 있고, 상속 대신에 구조적인 재사용 컴포넌트 형태로 사용하는 것을 추천한다.  
해당 포스트에서는 개발자가 React를 사용하면서 생각할 수 있는 상속에 대한 문제를 구조적으로 풀어가는 방법을 알아보려고 한다.  

### Containment  
React 컴포넌트는 `children`이라는 props를 가지고 있다.  
`children`은 해당 컴포넌트는 알 수 없는 자식 컴포넌트이며, 아래와 같이 사용된다.  

```javascript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

위 예제에서 보면 `FancyBorder` 컴포넌트는 알 수 없는 자식 컴포넌트인 `props.children`을 렌더링하고 있다.  
그리고 아래에 `WelcomeDialog` 컴포넌트에서 `FancyBorder`를 렌더링하며 하위에 `h1`, `p` 자식 컴포넌트(JSX tag)를 주었다.  
이러한 구조로 자식을 전달하여 렌더링이 가능하다.  

또한 `children` props를 사용하지 않고 원하는 props를 지정하여 직접 전달하는 방법도 가능하다.  
이러한 자식 컴포넌트를 패스하는 형식은 제한이 없다.  

```javascript
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

### Inheritance  
React을 만든 Facebook에서 말하길, 천여개의 컴포넌트들을 만들었지만 어떠한 형태로 상속을 구현하라고 추천하지 못한다고 말한다.  
필요할 경우 props와 컴포넌트 구조를 통하여 상속의 모습을 구현하되, props는 알 수 없는 형태도 전달이 가능하다는 점을 기억해야 한다.  
그것이 컴포넌트 일수도 있고 함수일수도 있다.  

***
