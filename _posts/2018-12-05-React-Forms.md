---
layout: post
title: "React Forms"
subtitle: "About React Forms"
background: "/background.jpg"
---

# React Forms

***

## 배경지식
javascript, React

***

## Forms  
React에서 폼(`form`)과 HTML에서 폼은 조금 다르게 작동되는데, 폼은 당연히 내부적인 `state`를 가지기 때문이다.  
HTML에서의 폼은 사용자가 입력한 데이터를 전송하는 역할을 한다.  
기본적으로 React에서도 HTML에서 사용하던 것처럼 동작한다.  
하지만 대부분의 경우 데이터를 전송하는 기능을 Javascript 함수 내에서 처리하는 것이 더 편리하다.  
이러한 기법을 일반적으로 말할 때 "Controlled Components"라고 한다.  

### Controlled Components  
HTML에서는 `<form>`태그 내부에 `<input>`, `<textarea>`, `<select>` 태그들은 각자 하나의 상태를 가지고 사용자의 입력을 업데이트한다.  
React에서는 여러 상태들을 컴포넌트의 `state`에 가지고 있고 `setState()` 메소드로 업데이트한다.  
결론부터 말하자면 React에서는 **폼의 구성을 컴포넌트화 하는 것**을 권장하고 있다.  

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

NameForm 컴포넌트에서는 `<form>`, `<input>` 태그를 통해 사용자의 입력을 받는다.  
입력은 `onChange`로 전달된 `handleChange()` 메소드에서 처리된다.  
여기서 입력받은 값을 변형하거나 검증할 수 있다.  
만약 입력받은 값을 전부 대문자로 변형하고 싶다면 아래와 같이 처리할 수 있다.  

```javascript
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```

개인적인 생각으로는 React에서는 폼을 사용하지 않거나, 편리한 오픈소스 UI 컴포넌트들을 활용하는게 좋을 것 같다.  

***
