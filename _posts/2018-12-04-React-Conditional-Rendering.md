---
layout: post
title: "React Conditional Rendering"
subtitle: "About React Conditional Rendering"
background: "/background.jpg"
---

# React Conditional Rendering

***

## 배경지식
Javascript, React

***

## 조건부 렌더링(Conditional Rendering)  
React Documents [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html) 문서를 기준으로 이해한 내용을 정리하였다.  

React 컴포넌트는 필요한 행동들을 캡슐화한다.  
이는 컴포넌트를 재사용할 경우 `props`를 통해서, 사용자의 상호작용을 통해서만 컴포넌트를 제어할 수 있다는 의미로 해석된다.  
컴포넌트에서 이러한 동적인 행동을 취하기 위해서는 아래와 같은 조건부 렌더링이 필요해진다.  

### Props를 활용한 조건부 렌더링  
아래는 조건부 렌더링의 예제이다.  
`UserGreeting`, `GuestGreeting` 두 함수형 컴포넌트를 만들었고 `Greeting` 함수형 컴포넌트에서 사용한다.  
`isLoggedIn` props를 통해 `UserGreeting`, `GuestGreeting` 두 컴포넌트 중 하나를 렌더링한다.  

```javascript
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

### state를 활용한 조건부 렌더링  
Javascript에서 조건문(`if`)를 사용하듯이 React에서도 동일하게 조건문을 작성하여 렌더링 할 수 있다.  
아래의 예제에서는 `isLoggedIn` state를 통해 로그인/로그아웃 버튼을 구현하였다.  
```javascript
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}

class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

조건부 렌더링에서 `props` 혹은 `state`를 활용하는데 이는 조건이 변경되었을 때 React Lifecycle에 의해 다시 렌더링하기 위함이다.  

### 인라인 조건부 렌더링  
Javascript에서 사용하는 `&&` 연산자를 활용하여 컴포넌트를 필요한 경우에만 렌더링할 수 있다.  
아래의 예제에서는 `unreadMessages` 배열의 길이가 0보다 큰 경우에만 문구를 렌더링하는 것을 확인할 수 있다.  
```javascript
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

### 인라인 삼항 조건부 렌더링  
Javascript에서 사용하는 삼항 연산자를 활용하여 컴포넌트를 렌더링하는 방법이다.  
`condition ? true : false` 형태의 연산자를 아래와 같이 예제처럼 활용할 수 있다.  
```javascript
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}

render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

### 컴포넌트 렌더링 방지  
컴포넌트를 조건에 맞게 렌더링하는 방법 중 하나이다.  
함수형 컴포넌트의 경우 반환 값을 `null`로, 클래스형 컴포넌트의 경우 `render()` 함수의 반환 값을 `null`로 처리한다.  


```javascript
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```

***
