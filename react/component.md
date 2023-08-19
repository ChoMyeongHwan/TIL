# Component
## 1. JSX
- JSX는 JavsScript의 확장 문법으로 JavaScript에서 HTML의 markup(태그) 방식처럼 엘리먼트를 생성하여 Component를 만들 수 있음
- 공식적인 JavaScript 문법이 아니므로 **바벨(babel)** 이라는 트랜스파일링 툴을 필요로 함
### babel
- ES6 코드(상위)를 이전 웹 브라우저 및 환경에서 돌아 갈 수 있는 하위 버전 코드로 변경(호환, Cross Browser)해주는 transpiler
- **JSX를 처리하기 위한 표준**
### JSX 활용
- JSX 문법 내에서는 **중괄호를 활용**하여 JavaScript 표현식을 적용할 수 있음
- Fragment를 활용한 element 생성
    + React의 엘리먼트는 **최상위 노드는 하나로만 구성**해야 함(하나의 DOM Tree로 작성)
    + React.Fragment 축약 문법
    ```javascript
    const element = (
        <>
            <h1>My favorite fruit is a</h1>
            <h3>Apple</h3>
        </>
    );
    ReactDOM.createRoot(document.getElementById('root')).render(element);
    ```
    
### attribute
- class 속성은 **className**이라는 속성명을 사용
- inline 방식으로 style를 적용할 때 **JavaScript의 객체**를 활용할 수 있음
    + css속성명은 camel-case로 작성
- JSX를 활용한 element 작성 시 중괄호를 활용하여 이벤트를 작성할 수 있음
- comment-in-JSX
    + 중괄호를 활용하여 주석을 작성
    + 태그 안에서 주석을 작성
