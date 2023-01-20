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
ReactDOM.render();
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
"span", { id: "sexy-span" }, "hello i'm a span";
```

- change style

```js
style: {
  color: "red";
}
```

-> 지금까지의 방법은 잘 쓰진 않지만 핵심임.

## `render`

- span과 button 두개를 랜더 하고싶을 때 (div 생성하기)

```js
const container = React.createElement("div", null, []);
```

-> 배열안에 span, btn을 둔다.

-> div를 render하는데, 그 안에 span, button 이 있음.

## `event listener`

- property에 id, className, style외에 eventListener도 등록가능함.

```js
const btn = React.createElement(
  "button",
  {
    onClick: () => console.log("i am  clicked"),
  },
  "Click me"
);
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
const title = (
  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
    hello i'm a title
  </h3>
);
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

-> 아직까진 콘솔창 오류

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
};
```

- Title을 렌더링 하고싶다면 대문자로 div안에 Title 작성

```js
const Container = (
  <div>
    <Title /> <Button />
  </div>
);
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
  </div>
);
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
function countUp() {
  counter = counter + 1;
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
ReactDOM.render(<Container />, root);
```

- 페이지를 로드 했을 떄, 이 코드가 바로 실행됨 .
- Container를 리랜더링 해서 다시 보여줘야하는데 말이지.

```js
function countUp() {
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
function countUp() {
  // 그 값을 바꾸는 함수
  //code
}
```

```js
const food = ["tomato", "potato"];
// 만약 food 외부에서 tomato 값을 받으려면 food[0]사용하면 되지만, 이걸 사용하고 싶으면 tomato같은 변수에 담아줘야함.
const tomato = food[0];
const potato = food[1]; //so bad
```

```js
// better
const food = ["tomato", "potato"];
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
modifier(3245235);
// 저번 시간에는 직접 랜더링 하고 값을 직접 바꾸고 리렌더링도 직접 했음.
```

```js
modifier(3245235);
counter = 345234535;
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
setCounter(counter + 1);
//여기에서 현재의 counter값을 가지고 계산해주고 있음.
//만약 현재 값을 가지고 계산을 해야한다면
setCounter(); //함수를 넣을 수도 있음.
//이 함수의 첫 번째 argument는 현재 값임.
```

```js
setCounter((current) => current + 1);
//seCounter함수가 뭘 return하든지 그게 새로은 state가 됨.
//리액트가 이 current가 확실히 현재 값이라는 걸 보장하고 있음.(우리가 정확히 원하는 값으로 계산할 수 있도록.)

// setCounter(counter +1); 와 동일하지만 위에것이 더 안전함.
```

## `Input and state `

//unit conversion(단위변환)

- 분을 시간단위로 바꾸기

```js
<label for="minutes">Minutes</label>
```

- class(x) => className
- for(x) => htmlFor

- JSX에서는 다르게 표현해줘야 함.

```js
<script src="https://unpkg.react-dom@17.0.2/umd/react-production.min.js"> 을 쓰기 때문에 에러가 뜨진 않음.
```

### minutes에 필요한 state만들기

- React Js에서는 input은 'uncontrolled' (input의 value는 우리가 통제할 수 없다.)

```js
const [minutes, setMinutes] = React.useState()

<input
        value={minutes}
        id="minutes" placeholder="Minutetype="number" />
```

```js
const [minutes, setMinutes] = React.useState();
```

- first array item is value.
- 두 번째는 value를 수정하고 component를 새로고침 할 때 쓰는 함수임.

```js
onChange = { onChange };
```

- 이제 onChange라는 event를 리스닝 함.
- input에 변화가 생기면, onChange 함수를 실행해줄 것.

```js
const [minutes, setMinutes] = React.useState();
const onChange = (event) => {
        setMinutes(event.target.value);
        };
value={minutes} //어디서든 input의 value를 수정해줄 수 있음.

<h4>You want to convert {minutes} </h4>
```

- 우리가 입력한 input의 value를 바탕으로 component를 업데이트해주고 있음.

## `recap`

```js
const [minutes, setMinutes] = React.useState(0);
// 초기값은 0
//  setState의 결과는 array. [data, function]
```

```js
value = { minutes };
// input의 value를 state로 연결. 매우 유용함 어디서든 input의 value를 수정해줄 수 있기 떄문.

onChange = { onChange };
// onChange함수는 데이터를 업데이트 해주는 역할을 함.(input에서 리스닝 하는 데이터)
// 보다시피 input은 스스로 업데이트를 함.

// change이벤트가 일어났을 때, 즉 사용자가 input에 뭔가를 써넣을 때 onChange함수가 실행됨.
// event.target.value를 얻게 되는데 바로 input vaule임.
// input의 value를 연결시켜주는 이유는 input값을 외부에서도 수정해주기 위함.
```

```js
onChange = { onChange };
//가 사라진다면 input에 작성이 안됨.
// 이유는 input의 value가 state이고, 이 state의  default값이 0이기 때문임. (useState(0);)
```

- 시간을 분단위로 설정하기

```js
<label htmlFor="hours">Hours</label>
       <input
       value={minutes /60}
       id="hours" placeholder="Hours" type="number" />
    //이 state를 60으로 나눠서 보여주는 것.
    // hours vaule만 리렌더링 됨
    // onCHange event가 없기 때문에 작성이 안됨.
```

```js
value={Math.round(minutes /60)} //이렇게도 가능(반올림)
```

- disabled 속성을 쓰면 작성이 안됨.

### `flip function`

- 반대로 변경시켜 줌.
- 새로운 state가 필요함.

```js
const [flippd, setflipped] = React.useState(false);
```

```js
<button onClick={onFlip}>Flipped</button>
```

- onFlip효과를 가진 버튼을 누르면 이 filpped값을 반전시키는 것.
- 만약 flipped이 ture상태라면, false를 반환하는 것.

```js
const onFlip = () => setFlipped(!flippd);
//better
const onFlip = () => setFlipped((current) => !current);
```

```js
disabled={flipped === true}
disabled={flipped} //same

 disabled={flipped === false}
 disabled={! flipped} //same
```

- hours input엔 아직 작성이 안됨. onChange를 넣어도 완벽히 안됨.(input에 뭘 써놓아도 (Math.round(minutes /60))이렇게 계산)

- 삼항연산자 이용

```js
   value={filpped ? minutes : Math.round(minutes /60)}
   //만약 filpped상태가 아니라면 변환된 값을 보여줘
```

### `Final Parctice and Recap`

```js
function MinutesToHours() { ....}

    function App() {
        return (
            <div>
                <h1>Super Converter</h1>
                {/* 분할정복(divide and conquer) */}
                <MinutesToHours />
            </div>
        );
    }
    const root = document.getElementById('root');
    ReactDOM.render(<App />, root);
</script>
```

- select

```js
function App() {
  const [index, setIndex] = React.useState(0);
  const onSelect = (event) => {
    setIndex(event.target.value);
  };
  return (
    <div>
      <h1>Super Converter</h1>
      <select value={index} onChange={onSelect}>
        <option value="0"> Minutes & Hours </option>
        <option value="1"> Km & Miles </option>
      </select>
    </div>
  );
}
const root = document.getElementById("root");
ReactDOM.render(<App />, root);
```

    - state를 변화시킬때 모든게 Rerender.

### `Props`

- props = 일종의 방식. 부모 컴포넌트로부터 자식 컴포넌트에 데이터를 보낼 수 있게 해주는 방법.
- MinutesToHours, KmToMiles = 자식 컴포넌트 (이 두 컴포넌트는 독립적임)
- component 는 단지 function일 뿐이야.

- 함수형 컴포넌트

```js
function ConfirnBtn() {
  return <button>Confirm</button>;
}
```

- JSX의 내부

```js
<div>
  <SaveBtn />
  <ConfirnBtn />
</div>
```

```js
function SaveBtn() {
  return;
  <button
    style={{
      backgroundColor: "tomato",
      color: "white",
      padding: "10px 20px",
      borderRadius: 10,
      border: 0,
    }}
  >
    Save Changes
  </button>;
}
function ConfirnBtn() {
  return (
    <button
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0,
      }}
    >
      Confirm
    </button>
  );
}
function App() {
  return (
    <div>
      <SaveBtn />
      <ConfirnBtn />
    </div>
  );
}
```

- 이렇게 하나씩 복붙하는건 좋지않은방법

```js
function Btn(props) {
  return (
    <button
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0,
      }}
    >
      {props.text}
    </button>
  );
}

function App() {
  return (
    <div>
      <Btn text="Save Changes" />
      <Btn text="Continue" />
    </div>
  );
}
```

- 대신 props는 오브젝트이기 때문에 우린 "{}"중괄호를 연다

```js
 function Btn({text}) {
  return (
    <button style={{
      backgroundColor: "tomato",
      color: "white",
      padding: "10px 20px",
      borderRadius: 10,
      border: 0,
    }}
    >
      {text}
    </button>
  );
```

- 두번째 인자로 big={}넣을 수 있다
- console창 -> Save Changes true
  Continue false

```js
function App() {
  return (
    <div>
      <Btn text="Save Changes" big={true} />
      <Btn text="Continue" big={false} />
    </div>
  );
}
```

- fontSize: big ? 18 : 1 (폰트사이즈가 빅이면 18 아니면 1)

### `Memo`

```js
<Btn text={value} onClick={changeValue} />
// onClick={changeValue} 은 하나의 Props 이름일뿐. 이벤트리스너를 추가시키는게 아님.
// 이벤트는 html태그에 달아야함.
```

- 내가 만약 여기 prop 이름을 onClick 으로 바꾼다고 한다면

```js
  return (
    <div>                 //👇
      <Btn text={value} onClick={changeValue} />
      <Btn text="Continue" />
    </div>
  );
}
```

```js
                  //여기로 onClick을 받고,
  function Btn({ text, onClick }) {
      return (
        <button
          // 여기에도 onClick이라 적어야함.
          //이걸 지워버린다면, ReactJS는 이 onClick을 button에 붙여주지 않음.
          onClick={onClick}

```

- 왜냐, onClick이라는 이름의 prop을 사용하고 있기 떄문.
- 또한 그 prop을 button 태그가 갖고 있는 onClick 이벤트리스너로서 사용하고 있기때문.
- prop들을 내가 원하는곳에 직접 넣어야만 함.
- onClick이라고 불리는 이벤트리스너와 완전히 동일한 이름일지라도. 이건 prop일 뿐.

```js
<html>
  <body>
    <div id="root"></div>
  </body>
  <!-- import react, react dom -->
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    // Memo
    function Btn({ text, onClick }) {
      console.log(text, "was rendered");
      return (
        <button
          onClick={onClick}
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            borderRadius: 10,
            border: 0,
          }}
        >
          {text}
        </button>
      );
    }

    function App() {
      {/* state */}
      {/* value가 Save Changes로부터 Revert Changes로 바뀜 */}
      const [value, setValue] = React.useState("Save Changes");
      const changeValue = () => setValue("Revert Changes");
      return (
        <div>
          {/* props */}
          {/* state가 변경된다면 props도 변경되어야함. */}
          <Btn text={value} onClick={changeValue} />
          <Btn text="Continue" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);

  </script>
</html>
```

- 만약 컴포넌트가 상태를 바꾼다면 다시 렌더링 하리란 것을 알고있음.
- 여기에선 부모가 state를 변경하고있고, 모든게 다시 그려짐 (Btn,Continue모두가). 하지만 continue가 리랜더링 되는걸 원치않음.
- 이걸로 React Memo 라고 불리는 걸 할 수 있음.(마치 기억하는 것처럼)
- 첫번째 Btn이 바뀌지 않는 조건으로 두번째 Btn이 리랜더링 되지않게.

```js
<div>
  <MemorizedBtn text={value} onClick={changeValue} />
  <MemorizedBtn text="Continue" />
  {/* continue는 다시 그려지지 않음.  */}
</div>
```

### 만약 부모가 어떤 state라도 변경이 있다면, 모든 자식들은 다시 그려지게 됨. (이게 추후에 어플리케이션이 느려지는 원인이 될 수 있음.) 그렇기 때문에 ReactJS에게 이 props가 변경되지 않는 다면 다시 그리지 않아도 된다고 말해주는 것 -> memo()

### `Prop Types`

- 문제는 컴포넌트에 매우 많은 props를 가질 떄 생김.
- React는 우리가 text에 무엇을 받고싶어하는지 모름. (우리는 text가 string이 되길 원하고, fontSize는 number가 되길 원함.) -> Prop Types라는 패키지가 있음.
- Prop Type은 어떤 타입의 Prop을 받고 있는지를 체크해줌.

```js
// 추가해주기
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>;

Btn.propTypes = {
  text: PropTypes.string,
  fontSize: PropTypes.number,
};
```

- ui에서는 에러를 보이지 않지만 콘솔창에서 말해줌.
- Prop Types: 다양한 테스트로 확인해볼 수 있음.

```js
// isRequired
Btn.propTypes = {
  text: PropTypes.string.isRequired,
  fontSize: PropTypes.number.isRequired,
};
```

### 틀렸을 떄 콘솔창

```js
Warning: Failed prop type: Invalid prop `fontSize` of type `string` supplied to `Btn`, expected `number`.
```
