---
layout: post
title: "React Context API"
subtitle: "About React Context API"
background: "/background.jpg"
---

# React Context API

***

## 배경지식  
Javascript, React

***

## React Context API ?  
React Context API는 React 16.3 버전부터 정식적으로 지원하는 API이다.  
그 전에도 실험적인 API 형태로 제공하고 있었지만 정식으로 제공하는 API로 변경해주어야 한다.  
React Context API를 사용하기 위해서는 `createContext()` 함수를 호출해야 한다.  
`createContext()` 함수는 인자로 `defaultValue` 값을 받으며 이 값은 상위에 `<Provider/>` 컴포넌트를 찾지 못한 경우에만 사용된다.  
```javascript
const MyContext = React.createContext(defaultValue);
```

`createContext()` 함수는 `<Provider/>`와 `<Consumer/>` 컴포넌트를 반환한다.  
`<Provider/>` 컴포넌트는 발행(Publish), `<Consumer/>` 컴포넌트는 구독(Subscribe)에 해당한다.  
`<Provider/>` 컴포넌트의 `value=data`값을 지정하고 값이 변경될 경우 `<Consumer/>` 컴포넌트의 `data` 값이 반영된다.  
```javascript
const { Provider, Consumer } = MyContext;

render() {
    return(
        <Provider value={data} >
            <Consumer>
                { (data) => <p>{data}</p> }
            </Consumer>
        </Provider>
    );
}
```

React-Redux에서 `<Prodiver/>`, `conntect()` 형태로 사용하는 것과 같이 Context API에서는 `<Consumer/>` 컴포넌트를 HOC로 구현하여 사용하도록 한다.  
```javascript
function withConsumer(WrappedComponent) {
    return class extends React.Component {
        render() {
            return (
                <Consumer>
                    { (data) => <WrappedComponent {...this.props} data={data}/> }
                </Consumer>
            );
        }
    }
}
```

## Redux vs Context API  
Redux 혹은 React Context API를 사용하기 전 장단점을 비교하여 사용해야 한다.  
Redux는 러닝커브가 길고 지켜야할 규칙이 많지만 많은 강력한 장점들이 있다.  
Context API는 러닝커브가 짧고 규칙은 없지만 편리하게 사용하기 위해서는 초기에 개발 부담이 생긴다.  
Redux의 장점을 살리지 못한다면 Context API를 사용하되 Redux의 일부 장점이나 컨셉만 빌려와 구현하는 것도 좋다.  

## Reference  
1. [React Context API](https://reactjs.org/docs/context.html)  
2. [React Context API 파헤치기](https://velopert.com/3606)  
3. [React Context API로 Redux를 대체할 수 있을까](https://medium.com/@Dev_Bono/context-api%EA%B0%80-redux%EB%A5%BC-%EB%8C%80%EC%B2%B4%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94-76a6209b369b)  
4. [Redux가 필요한가](https://medium.com/@Dev_Bono/%EB%8B%B9%EC%8B%A0%EC%97%90%EA%B2%8C-redux%EB%8A%94-%ED%95%84%EC%9A%94-%EC%97%86%EC%9D%84%EC%A7%80%EB%8F%84-%EB%AA%A8%EB%A6%85%EB%8B%88%EB%8B%A4-b88dcd175754)  

***
