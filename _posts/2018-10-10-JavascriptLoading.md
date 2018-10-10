---
type: post
title: "Javascript Loading"
---

1. HTML에서 Javascript 로드 방식
    1. inline
    태그에 Javascript를 기술하는 방식이다. 
    직관적이기 때문에 소규모 프로젝트에서는 유용하겠지만, 대규모 프로젝트의 경우 유지보수에 어려움을 야기할 수 있다. 
    ```HTML
    <body>
    <input type="button" onclick="alert('Hello World')" value="hello" />
    </body>
    ```
    위 HTML 코드 중 `alert('Hello World')` 부분이 Javascript 부분이며, `onclick` 이벤트에 의해 실행된다. 

    2. script
    `<script>` 태그 내에 Javascript를 기술하는 방식이다. 
    ```HTML
    <script src="test.js">
    ```
    위와 같이 사용하면 test.js 파일로부터 Javascript로 기술된 코드를 가져오게 된다. 

    3. script(From File)
    `<script>` 태그 내에 Javascript를 기술한 내용을 외부파일로 읽어드리는 방식이다. 
    ```HTML
    <script>
        ...
    </script>
    ```
    
    4. script(CDN, Contents Delivery Network)
    `<script>` 태그를 사용할 경우, 
    ```HTML
	<script src="http://...">
	```
	위와 같이 URL을 통해 Javascript Library를 다운로드하고 로드한다. 

2. HTML에서 Javascript 로드 위치
    1. `<head>` 태그 내부
    2. `<body>` 태그 내부
    결론적으로 `<body>` 태그 내부, 가장 하단에 위치하는 것이 가장 좋은 방법이다. 
    `<head>` 태그 내부에 위치할 경우 페이지가 로드되는 것을 기다리기 위해 아래와 같은 처리가 필요하다. 
    ```HTML
    <head>
    window.onload = function() {
	   ...
	}
	</head>
	<body>
		...
	</body>
	```
