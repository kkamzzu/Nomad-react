## REACT

## `react rules`

- import 하기
```js
<script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
```
```js
<script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
 ```
- react-dom은 React element 를 HTML에 두는 역할을 함.
- html을 페이지에 직접 작성하지 않음.

```js
ReactDOM.render()
```
- render = React element를 가지고 HTML을 만들어 배치한다는 것.(사용자에게 보여준다.)

```js
    <body>
        <div id="root"></div>
    </body>
``` 
- 이제 reactDOM에게 span을 root안에 두라고 하는 것. 

- 아직 span이 비어있음. createElement에는 더 작성할 수 있는 argument가 있음.

("span",{}) -> 두 번째 인자로 가능한 것은 spand의 property들임.

- property는 class name이 될 수 있고, id가 될 수도 있음. 

```js
ex)

('span',{id: "sexy-span"})
```

- 아직 span은 비어있음.(content는 createElement의 세 번째 argument로 들어갈 것.)

- 세 번째 argument는 span의 내용.
```js
('span',{id: "sexy-span"},"hello i'm a span")
```

- change style
```js
style:{color: "red"}
```

-> 지금까지의 방법은 잘 쓰진 않지만 핵심임. 

## `render`

- span과 button 두개를 랜더 하고싶을 때 (div 생성하기)
```js
const container = React.createElement('div', null, [])
```
-> 배열안에 span, btn을 둔다.

-> div를 render하는데, 그 안에 span, button 이 있음.

## `event listener`

- property에 id, className, style외에 eventListener도 등록가능함.

```js
 const btn = React.createElement('button', {
            onClick: () => console.log('i am  clicked')}, "Click me");
```            

- addEventListener 를 반복하는 것 대신, property에서 event를 등록할 수 있게 됨.

## `recap(1)`
- react js, react dom import.
- react JS는 (must have) element를 생성하고 event listner를 더하는 것을 도와줌.
- react-dom은 React element 를 HTML에 두는 역할을 함.
- BUT, createElement를 쓸 일은 없음. 더 쉬운 방법이 있지만 이게 기초.
- 첫 번째 argument는 root에 들어갈 HTML tag.
- 두 번째 argument는 props가 포함된 object.
- 두 번쨰 argument는 'on'으로 시작하는 유효한 event가 있어야 함. (very powerful!)
- 세 번째 argument는 content.


## `JSX (javaScript를 확장한 문법)`
- creacteElement를 대체하려는 이유: 좀 더 편리한 도구를 사용하기 위함. -> JSX

```js
     const title = <h3 id="title" onMouseEnter={() =>   console.log("mouse enter")}>
            hello i'm a title</h3>
```
- html 과 똑같이 생김.
- props는 태그안에.
- onMouseEnter는 마치 태그가 가진 하나의 속성인 것처럼 추가하면 됨. (굉장히 편리함) 
- BUT 여기서 콘솔창에 에러가 남 : 브라우저가 온전히 JSX를 이해하는 것은 아니기 떄문.
- 이해할 수 있게 'babel'설치를 해줘야함. 
- babel은 코드를 변환시켜주는 것.
```js
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```
->  아직까진 콘솔창 오류
```js
<script type="text/babel"></script>
```
-> 넣어주기

## `JSX (2)`

- 타이틀이나 버튼을 포함시키기 위해 해야할 것은 const Button을 함수로 만들어줘야함.
```js
 const Button = () => (
```
- 그리고 return을 해줘야함 (매우 종요)
```js
 const Title = () => {
            return (
                <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
                    hello i'm a title
            </h3>
            );
        }
```        
- Title을 렌더링 하고싶다면 대문자로 div안에 Title 작성
```js
   const Container = (
            <div> 
                <Title /> <Button /> 
            </div>) ;
        
```        
- 코드를 붙여넣기 한다고 생각.
- 컴포넌트의 첫 글자는 반드시 대문자여야 함. (중요)
```js
<Title />  

// 만약 소문자라면 React랑 JSX는 이게  HTML button 태그라고 생각함.
```

## `React.js 의 state`

- state는 기본적으로 데이터가 저장되는 곳. 
```js
// 버튼을 3번 랜더링
 const Container = () => (
            <div> 
                <Title /> 
                <Button /> <Button /> <Button />
            </div>) ;
```
-> 함수의 형태이기 떄문이고, 이게 동일한 코드를 재사용 할 수 있는 방법.             

- React.js코드 내에서 카운트를 셀 수 있게 만들기.
- 두가지 방법
- (1) : 안좋은방법
- (2) : 좋은방법
- 단지 중괄호를 열어주면 변수이름을 넣으면 끝
```js
<h3>Total clicks: {counter}</h3>
``` 

- 카운트를 하는 함수 만들기
```js
function countUp(){
            counter = counter + 1 
        }

  const Container = () => (
            <div> 
                
                <h3>Total clicks: {counter}</h3>
                <button onClick={countUp}>Click me</button>
            </div>
        );
```                    
-> UI 가 업데이트 되지 않아서 클릭 수가 뜨지않음.
->console.log(counter) 로 확인하기.

- 함수는 바로 실행되지 않음.
```js
ReactDOM.render(<Container />, root)
```
- 페이지를 로드 했을 떄, 이 코드가 바로 실행됨 .
- Container를 리랜더링 해서 다시 보여줘야하는데 말이지.
```js
   function countUp(){
            counter = counter + 1;
            ReactDOM.render(<Container />, root); //리랜더링
        }
```        

- 정리 
```js

// 어플리케이션이 시작하면 카운터는 0 

// 랜더 함수를 실행

// render함수는 Container 컴포넌트를 root에 담아줄 것. 

// 어플이 막 시작되었을 때의 Container는 Total click을 가지고 있고 counter와 연결되어 있음.

// 이벤트리스너를 등록하면 버튼 클릭시 카운트 업 함수가 실행 됨. 

// 카운트업은 카운트를 증가시키고 다시 render를 호출해줌.

// render 함수가 호출되면 똑같은 과정이 반복됨.

// 계속해서 render해주는 것은 좋은 방법이 아님.

// 리액트는 인터렉티브한걸 만들기에 최적화 되어있음.

// 우리가 새로 랜더링 하더라도 전체를 전부 재생성할 필요없이 바뀐부분만 새로 생성할 수 있게 도와줌. 
```

## `better than rerendering: useState()`

- 함수 내에서 return문 전에 상수를 하나 만들어 줌.
```js
 const data = React.useState();
 console.log(data); //(2) [undefined, ƒ] 배열을 받음.
 ```
 - undefined -> data
 - ƒ -> data를 바꿀 때 사용하는 함수
 - React.useState() 함수는 초기값을 설정할 수도 있음.
 ```js
 const data = React.useState(0); //초기값 = 0 -> [0, ƒ]
 ```

- [0, ƒ] 이 두 요소가 만나서 countUp 함수의 역할을 대신해주고 있음.
```js
let counter = 0; //초기값
function countUp(){ // 그 값을 바꾸는 함수
    //code
}
```

```js
const food = ["tomato", "potato"]
// 만약 food 외부에서 tomato 값을 받으려면 food[0]사용하면 되지만, 이걸 사용하고 싶으면 tomato같은 변수에 담아줘야함.
const tomato = food[0]
const potato = food [1]  //so bad
```

```js
// better 
const food = ["tomato", "potato"]
const [myFavFood, mySecondFavFood] = food;
// myFavFood = 'tomato'
// mySecondFavFood 'potato'

const [counter, modifier] = React.useState(0);

```
## `useState() - 2`
<!-- 왜 modifier가 필요하고 어떻게 쓸건지 -->

- modifire() 함수는 값을 하나 받음
- 어떤 값을 부여하든 modifier 함수는 그 값으로 업데이트하고 리렌더링을 일으킴.
```js
modifier(3245235)
// 저번 시간에는 직접 랜더링 하고 값을 직접 바꾸고 리렌더링도 직접 했음.
```
```js
modifier(3245235);
counter =345234535
ReactDOM.render(<App />, root); //rerender
//이모든게 modifier 함수 내에서 자동으로 일어날 것.
// 컴포넌튿오 동시에 rerendering. 업데이트 완료
```
- [counter, setCounter] set을 붙여줌. 

- modifier 함수를 사용해 state, 즉 어플리케이션의 데이터를 바꿀 때 modifier 함수로 state를 바꿀 때, 컴포넌트 전체가 재생성 됨.

- 이 방법이 그다지 좋은 방법은 아님. counter는 다른 곳에서 update 될 수 있기 때문.(counter가 다른 곳에서 변경 되어 우리가 생각했던 값이 아닐 수 있음)

## `State Functions`
<!-- 앱의 state 를 바꾸는 법 -->

```js
   setCounter(counter +1);
    //여기에서 현재의 counter값을 가지고 계산해주고 있음.
    //만약 현재 값을 가지고 계산을 해야한다면
    setCounter() //함수를 넣을 수도 있음.
    //이 함수의 첫 번째 argument는 현재 값임.
   ```
   ```js
   setCounter((current)=> current +1)
   //seCounter함수가 뭘 return하든지 그게 새로은 state가 됨. 
   //리액트가 이 current가 확실히 현재 값이라는 걸 보장하고 있음.(우리가 정확히 원하는 값으로 계산할 수 있도록.)

   // setCounter(counter +1); 와 동일하지만 위에것이 더 안전함.
   ```