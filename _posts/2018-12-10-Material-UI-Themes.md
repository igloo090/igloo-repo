---
layout: post
title: "Material-UI Themes"
subtitle: "About Material-UI Themes"
background: "/background.jpg"
---

# Material-UI Themes  

***

## 배경지식  
javascript, React

***

## Material-UI Themes  
Material-UI(이하 MUI)에서 테마(Theme)라는 컴포넌트 스타일링 방식을 제공한다.  
테마는 어플리케이션의 색상(색조)을 일정하게 적용해주므로 비즈니스나 브랜드에 맞게 커스터마이징을 할 수 있다.  
테마는 밝은 타입, 어두운 타입을 제공하고 밝은 타입이 기본값으로 적용된다.  

### Customize Themes  
테마를 원하는 대로 바꾸기 위해서는 `MuiThemeProvider` 컴포넌트를 사용한다.  
`MuiThemeProvider` 컴포넌트는 React의 Context API를 활용하여 테마 정보를 하위 컴포넌트로 전달한다.  
그렇기 때문에 원하는 테마를 적용시키기 위해서는 `MuiThemeProvider` 컴포넌트를 가장 상위에 위치시켜야 한다.  

대표적인 테마 속성은 아래와 같다.  
1. Palette
2. Type (light/dark theme)
3. Typography
4. Other variables
5. Custom variables  

### Palette  
먼저 팔레트(Palette)를 이해하기 위해서는 Material Design에서 말하는 [Color System](https://material.io/design/color/the-color-system.html#color-usage-palettes)에 대해서 알아야 한다.  
Material Design Palettes는 Primary Color, Secondary Color 그리고 Light/Dark Variants로 구성된다.  
색상과 밝기의 조합으로 팔레트를 구성하고 어플리케이션에 적절하게 적용하는 컨셉이다.  
Primary Color는 어플리케이션에서 가장 빈번하게 사용되는 색상이다.  
만약 Secondary Color가 없을 경우 강조에서도 사용된다.  
Secondary Color는 어플리케이션에서 강조하거나 구분할 때 사용되는 색상이다.  
컨트롤을 선택하거나 텍스트의 하이라이트 등 여러 중요한 액센트를 표현하고자 할 때 사용된다.  

팔레트는 위에서 설명한 것처럼 하나의 색상과 그 색상에 대한 밝기로 구성된다.  
만약 빨강(500)이라는 색상을 기준으로 보면 가장 밝은 색은 핑크(red 50)이고 가장 어두운 색상은 적색(red 900)이다.  
[Color Tool](https://material-ui.com/style/color/#color-tool)을 통해 Primary/Secondary 색상을 선택하면 우측에서 이에 대한 결과를 볼 수 있다.  

이제 어플리케이션에서 테마를 적용하는 방법을 알아본다.  
Color Tool에서 색상을 지정한 것처럼 `createMuiTheme` 함수를 사용하여 테마를 생성할 수 있다.  
생성된 테마를 `MuiThemeProvider` 컴포넌트의 `theme` 인자로 넘기면 테마를 적용할 수 있다.  

```javascript
import { createMuiTheme } from '@material-ui/core/styles';
import purple from '@material-ui/core/colors/purple';

const theme = createMuiTheme({
  palette: {
    primary: purple,
    secondary: {
      main: '#f44336',
    },
  },
});

<MuiThemeProvider theme={theme}></MuiThemeProvider>
```

만약 위의 예제처럼 테마를 적용했을 경우 제공한 Primary, Secondary를 제외한 테마 정보는 기본 테마로 적용된다.  
즉, 커스터마이징할 부분만 제공하면 나머지는 MUI에서 제공한다는 뜻이다.  

### Type (light/dark theme)  
테마의 타입은 Light/Dark가 기본적으로 제공되며 타입에 따라 내부적으로 특정 키들이 변경된다.  
전반적인 테마의 타입을 나타낸다고 말할 수 있다.  

### Typography  
MUI에서는 기본적으로 문자의 사이즈에 대해서 제한을 둔다.  
이러한 제한적인 규칙성은 어플리케이션의 일관된 레이아웃을 구성하도록 유도한다.  
제한은 강제적이지 않으므로 필요한 경우 원하는 문자를 구성하는 것도 가능하다.  

### Other variables  
다른 변수들에 대해서는 [기본 테마 정보](https://material-ui.com/customization/default-theme/)에서 확인할 수 있다.  

### Custom variables  
해당 부분은 [Custom Variables](https://material-ui.com/customization/themes/#custom-variables) 문서의 예제의 소스코드를 분석하여 이해하는 것이 빠를 것 같다.  
예제는 `CheckBox` 컴포넌트를 테마의 Danger 기준으로 색상을 표현하는 소스코드이다.  

### withTheme  
`withTheme`는 컴포넌트에 `props`로 테마를 전달해주는 Higher-Order Component이다.  
전달된 `props`를 통해 컴포넌트를 렌더링하는 것이 가능하다.  

```javascript
import { withTheme } from '@material-ui/core/styles';

function MyComponent(props) {
  return <div>{props.theme.direction}</div>;
}

export default withTheme()(MyComponent);
```

## 마치며  
MUI는 Material Design을 기본으로 알고 있어야 한다고 생각된다.  
이번에 테마를 알아가면서 궁금증이 생겼는데, 어떻게 테마와 CSS를 적절하게 조합하여 어플리케이션을 구성할 수 있을까?  
테마를 쓰면서 CSS를 원하는대로 적용하려면 결국 CSS-in-JS, Javascript 내에 스타일링 코드가 들어가야 된다는 말일까?  
기본 값으로 어플리케이션을 구성하면 정말 개성없는 그런 어플리케이션이 될 것이 뻔하다.  
결국 스타일을 마음대로 조절하기 위해서 CSS나 Theme에 대한 이해도를 높여야 할 것 같다.  

***
