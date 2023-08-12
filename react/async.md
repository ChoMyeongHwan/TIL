# async
## 비동기(async)-넌블로킹(nonblocking)
- 메인 흐름은 멈추지 않는 상태에서 특정 작업들을 백그라운드에서 처리하여 **동시에 처리하는 것처럼 실행**함
- 비동기 작업을 할 때 가장 많이 사용하는 방식 -> **콜백 함수를 이용**
- 이전 함수의 호출 결과가 다음 함수에 반영되지 않음

## promise
- 콜백 지옥과 같은 코드가 형성되지 않게(비동기 통신 간에 순서를 정하기 쉽게) 하는 방안(ES6에서 도입)
- 최종 결과를 반환하는 것이 아닌 미래의 어떤 시점에 결과를 제공하겠다는 '**약속**'을 반환함
### promise의 상태
- 대기(pending) : 이행하지도, 거부하지도 않은 초기 상태
- 이행(fulfilled) : 연산이 성공적으로 완료된 상태
- 거부(rejected) : 연산이 실패한 상태
### resolve와 reject
- promise 객체는 resolve와 reject 함수를 활용함
1. resolve : 함수의 인자로 넘어온 값을 저장하고 있다가 then을 만나면 저장했던 값을 지닌 Promise 객체를 반환함
2. reject : 어떠한 이유로 거부되어야 할 때 Promise 객체를 반환함

## async-await
- promise 객체를 더 쉽게 사용할 수 있음
- **await 키워드를 사용**해서 **promise를 반환하는 함수를 호출**하면 해당 **promise의 resolve에 저장된 값이 반환**됨
- then을 사용하지 않고(`메소드 체이닝` 방식 없이) **비동기 처리 함수를 동기식으로 처리**할 수 있음
> 메소드 체이닝(Method Chaining)<br/>
연속적인 코드 줄에서 객체의 Method를 반복적으로 호출하는 것을 의미함<br/>
Method가 객체를 반환하면 그 반환 값(객체)이 또 다른 Method를 호출할 수 있음
### await의 두가지 기능
1. await가 달린 함수의 결과인 promise에 담긴 결과(promise 내부의 resolve에 담긴 결과)를 반환함
2. await가 달린 비동기 처리들은 동기식으로 동작하게 함

---

## API
- 자바스크립트를 사용해 **새로고침 없이(비동기식) 서버에서 새로운 정보**를 받아올 수 있음
- promise 객체 기반이 아닌 Ajax를 이용해서 비동기식으로 처리할 수 있음
- Ajax 외에도 fetch api를 이용할 수 있음
- promise 기반의 비동기 처리를 위해 axios.js를 쓸 수 있음

## fetch-async-await
- fetch 기본 사용 방법
```javascript
let promise = fetch(url, [options]);
/*
 * url : 접근하고자 하는 url
 * options : 선택 매개변수로 http method나 headers, body 내용을 객체로 지정 가능
 *           아무 값도 넣지 않으면 GET 메소드(8가지 http method 중)로 요청함
 * 
*/
```
- 예시
```javascript
// fake api 활용
async function callAPI() {
    const promise = fetch('https://jsonplaceholder.typicode.com/users');

    // async await를 활용해서 결과 객체 꺼내기
    const response = await promise;
    console.log(response);

    console.log(`응답 상태: ${response.status}`);

    console.log('응답 헤더');
    /* 
    response.headers에 대한 내용 중 일부는 
    숨김 프로퍼티([Symbol.iterator])라서 for of문으로 확인함 
    */
    for(let [key, value] of response.headers) {
        console.log(`${key}: ${value}`);
    }

    console.log(`본문 내용 사용 여부: ${response.bodyUsed}`);
}
```

## fetch-then
- async/await를 활용하지 않고 fetch의 반환 값인 promise가 제공하는 then 메소드를 활용하여 메소드 체이닝 방식으로 순차적인 비동기 요청 및 결과 값 확인 할 수 있음
- 예시
```javascript
function callAPI() {
    fetch('https://jsonplaceholder.typicode.com/users')
    .then((response) => {
        console.log(response);
        return response.json();
    }).then((json) => {
        console.log(json);
    });
}

function App() {
    const onClickHandler = () => {
        callAPI();
    }
    return <button onClick={onClickHandler}>API 요청</button>
}

ReactDOM.createRoot(document.getElementById('root')).render(<App/>);
```

## axios
- axios는 데이터 변환처리(json()) 등을 하지 않아도 되서 편리하게 사용 가능함
- 이미 파싱된 데이터가 data라는 조회 결과 response 객체의 프로퍼티로 들어있음
- ref : https://github.com/axios/axios#example
- 예시
```javascript
function callAPI() {
    axios.get('https://jsonplaceholder.typicode.com/users')
         .then(res => console.log(res.data))
         .catch(err => console.log(err));
}

function App() {
    const onClickHandler = () => {
        callAPI();
    }
    return <button onClick={onClickHandler}>API 요청</button>
}

ReactDOM.createRoot(document.getElementById('root')).render(<App/>);
```


