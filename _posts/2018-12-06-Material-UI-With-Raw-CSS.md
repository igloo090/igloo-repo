---
layout: post
title: "Google Material UI with Raw CSS"
subtitle: "About Google Material UI with Raw CSS"
background: "/background.jpg"
---

# Google Material UI with Raw CSS

***

## 배경지식
CSS, Javascript, React, Material-UI

***

## Material-UI
Material-UI(이하 MUI)는 Google에서 개발한 오픈소스 React UI Libarary이다.  
MUI에서는 기본적인 테마/스타일을 제공한다.  
허나 웹/앱을 개발하다보면 디자인은 제각각 다르고 천차만별이다.  
원하는 스타일을 입히기 위해서는 CSS를 사용해야 한다.  

개인적으로 React 컴포넌트와 가장 잘 맞는 방식은 CSS Modules인 것 같다.  
컴포넌트별로 CSS 파일을 분리하여 적용하고 재사용할 경우 원하는 컴포넌트의 .js, .css 파일만 가져오면 된다.  
그리고 Create-React-App 최신버전부터는 SCSS도 지원하므로 고려해볼만 하다.  
만일 가장 심플하고 간략하게 테스트용도로 CSS가 필요하다면 Inline CSS을 사용할 것 같다.  

해당 포스트는 Material-UI Document [Style Library Interoperability](https://material-ui.com/guides/interoperability/) 문서를 기준으로 작성되었다.  

다음 설명할 방법 중 CSS in JS(JSS)에 해당하는 방법이라면 [CSS in JS](https://material-ui.com/css-in-js/basics/)를 반드시 확인하길 바란다.  
또한 JSS는 `<head>` 태그 가장 아래에 `<style>` 태그가 들어가는데, `!important` 속성을 사용하지 않는다면 [the CSS injection order](https://material-ui.com/customization/css-in-js/#css-injection-order) 문서를 반드시 확인하길 바란다.  

### Raw CSS  
기존 Javascript에서 CSS를 적용하듯이 React에서도 컴포넌트에 `className`에 원하는 클래스를 지정하고 CSS를 입힐 수 있다.  
React에서는 regular DOM, SVG elements에는 `class` 대신 `className`을 사용한다.  
해당 내용은 React Document [className](https://reactjs.org/docs/dom-elements.html#classname)에서 확인할 수 있다.  

[CodeSendbox](https://codesandbox.io/s/vmv2mz9785)

### Styled Components  
Javascript 내에서 CSS를 입히는 방법 중 하나이다.  
MUI v3.6.1 기준 Alpha Version이므로 아직 사용하기는 이르다.  
MUI v4.x.x 버전이 나올 때 정식으로 포함될 경우 사용하는게 좋을 것 같다.  

[CodeSendbox](https://codesandbox.io/s/mzwqkk1p7j)

### Emotion  
Emotion.js를 사용하여 Javascript 내에서 CSS 입히는 방법 중 하나이다.  

[CodeSendbox](https://codesandbox.io/s/yw93kl7y0j)

### React Emotion  
Emotion과 동일하다.  

### CSS Modules  
Webpack이나 Parcel 등 빌드 도구를 이용하여 CSS를 입히는 방법이다.  

[CodeSendbox](https://codesandbox.io/s/m4j01r75wx)

### Global CSS  
MUI에서 지정되어 있는 `className`을 기준으로 CSS를 수정할 수 있다.  
공식적으로도 주의해야 할 사항들이 많으므로 사용하지 않는 것이 좋을 것이다.  

[CodeSendbox](https://codesandbox.io/s/2zv5m0j37p)

### React JSS  
React-JSS를 사용하는 방법이다.  

[CodeSendbox](https://codesandbox.io/s/219x6qqx0p)

### CSS to MUI webpack Loader  
Webpack의 로더 중 css-to-mui-loader를 적용하여 `withStyles()` HOC와 함께 사용하는 방법이다.  
MUI에서 설명하는 예제는 `withStyles()` 기준으로 작성되어 있고, CSS을 적절하게 조합할 수 있는 방법인 것 같다.  
다음은 Webpack 설정, CSS, Javascript에 대한 예제이다.  

```
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'babel-loader', 'css-to-mui-loader' ]
      }
    ]
  }
}
```

```css
.button {
  background: $(theme.palette.primary.main);
  padding: 2su; /* Material-UI spacing units */
}

.button:hover {
  background: $(theme.palette.primary.light);
}

@media $(theme.breakpoints.down('sm')) {
  .button {
    font-size: $(theme.typography.caption.fontSize);
  }
}
```

```javascript
import Button from '@material-ui/core/Button';
import { withStyles } from '@material-ui/core/styles';
import styles from './CssToMuiButton.css';

const CssToMuiButton = withStyles(styles)(({ classes }) => (
  <Button className={classes.button}>
    CSS to MUI Button
  </Button>
));
```

### Glamor  
Glamor를 사용하여 Javascript 내에서 CSS 입히는 방법 중 하나이다.  

[CodeSendbox](https://codesandbox.io/s/ov5l1j2j8z)

***

## Reference  
1. [What's the Best Way to Style React Components?](https://www.optasy.com/blog/what-best-way-style-react-components-4-most-widely-used-approaches-styling)

***  
