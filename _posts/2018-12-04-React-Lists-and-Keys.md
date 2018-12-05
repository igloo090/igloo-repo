---
layout: post
title: "React List and Keys"
subtitle: "About React List and Keys"
background: "/background.jpg"
---

# React List and Keys

***

## 배경지식  
Javascript, React  

***

## List and Keys  
React Documents [List and Keys](https://reactjs.org/docs/lists-and-keys.html) 문서를 기준으로 이해한 내용을 정리하였다.  
[Array Method](https://www.w3schools.com/js/js_array_methods.asp)에 대한 내용은 미리 숙지하고 이후로 넘어가길 권장한다.  

먼저 Javascript에서 배열을 조작하는 예제를 본다.  
```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

위 예제는 `numbers` 배열에 있는 값들을 2배로 만든 새로운 배열을 반환하여 콘솔에 출력한다.  
React에서도 거의 동일한 형태로 사용되며 단지 값(오브젝트)이 아닌 컴포넌트가 된다.  
실제로 **React의 컴포넌트는 결국 오브젝트이므로 동일**하다고 볼 수 있다.  

아래의 예제는 리스트를 화면에 출력한다.  

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

### 기본 리스트 컴포넌트  
아래는 기본적인 리스트를 렌더링하는 컴포넌트이다.  
`numbers` props로 배열을 전달받는 것으로 React Lifecycle에 의해 렌더링될 수 있다.  
```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

### Keys  
React에서 `key`(이하 키)는 어떤 아이템이 변경되었는지, 추가되었는지, 삭제되었는지 알려준다.  
키를 사용하는 가장 좋은 방법으로는 유니크한 ID를 사용하는 것이 좋다.  
단, Index를 사용하는 것은 리스트의 정렬이 바뀔 수 있으므로 권장하지 않는다.  
만약 아무런 키를 주지 않으면 기본 값으로 인덱스를 사용한다.  
즉, 리스트를 사용할 때 항상 키를 고려하여 개발하고 유니크한 값으로 지정해야 한다.  
```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

컴포넌트 내에 리스트를 렌더링할 경우 키는 `<li>`가 아닌 `<ListItem>` 컴포넌트에 지정해야 한다.  
```javascript
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

### 동일한 리스트에서 키는 항상 유니크한 값  
이렇게 사용해야 하는 이유는 [링크](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)를 통해 확인할 수 있다.  
> a key is the only thing React uses to identify DOM elements.  

[링크](http://jsbin.com/wohima/edit?js,output)에서 키를 ID와 Index로 사용하였을 때 문제점에 대해 실행하여 확인할 수 있다.  
리스트에 텍스트를 기입하고 버튼으로 리스트를 삽입하면 문제를 한눈에 확인할 수 있다.  

React에서 `key`는 DOM 요소를 구분하는 값으로 사용된다.  
만일 리스트의 중간에 아이템을 삽입하거나 제거할 경우 문제가 된다.  
동일한 ID의 아이템을 삭제하고 다시 삽입한 경우 React에서는 동일한 아이템이라고 간주하지 않는다.  

만약 내가 만든 리스트 컴포넌트에 ID를 전달하고 싶은 경우 `key`와 원하는 `props`(아래에서는 `id`)를 구분지어서 전달하도록 한다.  
키는 React에서 활용하기 때문에 건들지 않도록 하는게 좋은 방법이다.  
```javascript
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

### JSX 내부에서 리스트 표현  
```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

위 예제를 아래와 같이 사용해도 결과는 동일하다.  
본인에게 맞는, 혹은 프로젝트에 알맞는 표현 방식으로 사용하는 것이 좋다.  
```javascript
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />

      )}
    </ul>
  );
}
```

***
