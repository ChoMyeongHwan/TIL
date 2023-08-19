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

## 2. rendering
### rendering-element
- ReactDOM에서 관리하며 React의 엘리먼트들이 렌더링 될 하나의 DOM을 **Root DOM Node**라고 함
```javascript
// ReactDOM.createRoot(루트 DOM 노드).render(렌더링 할 엘리먼트)
ReactDOM.createRoot(document.getElementById('root')).render(element);
```

### rendered-element-update
- 리액트에서 엘리먼트를 바꿀 때는 **엘리먼트 단위로 변경** (불변객체, immutable)
- 엘리먼트는 특정 시점의 UI를 의미
- 기존의 가상 돔과 새로운 변화로 생성된 가상 돔(Render Tree를 기반으로 생성 된)을 통해 변화가 있는 부분만 변경이 일어남
### conditional-rendering
- 엘리먼트 생성 시점 혹은 렌더링 시점에 조건부를 활용하여 **조건에 따라 다른 엘리먼트가 렌더링** 될 수 있도록 작성 가능함

## 3. component
- 중복되는 엘리먼트들을 추상화해서 컴포넌트로 작성하고, 작성된 **컴포넌트를 재사용**하는 것이 리액트가 추구하는 한 가지 방향임
- state 사용 및 라이프 사이클 기능, 임의의 메소드 정의 등은 클래스 컴포넌트에서만 사용 가능한 방식
- 함수형 컴포넌트에서 유사한 개념으로 사용할 수 있는 훅스(hooks)를 제공
- 컴포넌트 활용 규칙
    + 앞 글자 대문자
    + 닫기 태그 존재
    + 클래스나 함수 이름과 동일
### 클래스형 컴포넌트
```javascript
// render() 함수를 포함하며 React.Component를 상속받는 클래스를 통해 컴포넌트를 정의할 수 있음
class Title extends React.Component {
    render() {
        return (
            <h1>Class Componenet</h1>
        );
    }
}


ReactDOM.createRoot(document.getElementById('root')).render(<Title/>);
```

### 함수형 컴포넌트
```javascript
// 함수의 반환값으로 ReactElement만 정의해서 반환(일반적으로 JSX 사용)
function Item() {
    return (
        <>
            <h2>상품1</h2>
            <h3>상품명: 휴대용 선풍기</h3>
            <h3>가격: 20000원</h3>
        </>
    );
}

ReactDOM.createRoot(document.getElementById('root')).render(<Item/>);
```

### 컴포넌트 합성
- 컴포넌트는 자신의 ReactElement 생성을 위해 다른 컴포넌트를 참조할 수 있음
- 컴포넌트는 재사용 가능한 크기로 작게 유지해야 하며, **순수 함수처럼 작성**되어야 함

## 4. props
- props는 properties를 줄인 약어로 **컴포넌트의 속성을 설정**할 때 사용
- 해당 컴포넌트를 포함한 부모 컴포넌트에서 설정해서 넘겨줌
- "모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 한다."
- `순수함수` : 동일한 입력 값에 대해 항상 동일한 결과를 반환하는 것(외부에 의존하지 않음)
- **컴포넌트는 반드시 순수 함수로 작성**
- **props는 읽기 전용 객체**
### props-destructuring-assignment
- props로 넘어올 때의 속성명과 컴포넌트 태그 사이 값을 **객체 구조분해 할당(Destructuring)** 을 통해 props의 속성에 접근하지 않고 간편하게 활용할 수 있음.
```javascript
function PropsPrinter({name, children}){
    return (
        <>
            <h3>아침에 먹은 {name}은(는)</h3>
            <h3> {children}이다.</h3>
        </>
    );
}

ReactDOM.createRoot(document.getElementById('root')).render(
    <PropsPrinter name="사과">내 스타일</PropsPrinter>
);
```

