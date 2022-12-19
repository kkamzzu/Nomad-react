#REACT

## (0) react rules

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
- render = React element를 가지고 HTML을 만들어 배치한다는 것.(사용자에게 보여주다.)

```js
    <body>
        <div id="root"></div>
    </body>
``` 
- 이제 reactDOM에게 span을 root안에 두라고 하는 것. 

- 아직 span이 비어있음. createElement에는 더 작성할 수 있는 argument가 있음.

("span",{}) -> 두 번째 인자로 가능한 것은 spand의 property들임.

- property는 class name이 될 수 있고, id가 될 수도 있음. 
ex)
```js
('span',{id: "sexy-span"})
```

- 하지만 아직 span은 비어있음.(그건createElement의 세 번째 argument로 들어갈 것.)

- 세 번째 argument는 span의 내용
```js
('span',{id: "sexy-span"},"hello i'm a span")
```

- change style
```js
style:{color: "red"}
```

-> 지금까지의 방법은 잘 쓰진 않지만 핵심임. 

## (1) render

- span과 button 두개를 랜더 하고싶을 때 (div 생성하기)
```js
const container = React.createElement('div', null, [])
```
->배열안에 span, btn을 둔다.
-> div를 render하는데, 그 안에 span, button 이 있음.

## (2) event listener

- property에 id, className, style외에 eventListener도 등록가능함.

```js
 const btn = React.createElement('button', {
            onClick: () => console.log('i am  clicked')}, "Click me");
```            

- addEventListener 를 반복하는 것 대신, property에서 event를 등록할 수 있게 됨.

### recap (1)
- react js, react dom import.
- react JS (must have) element를 생성하고 event listner를 더하는 것을 도와줌.
- react-dom은 React element 를 HTML에 두는 역할을 함.
- BUT, createElement를 쓸 일은 없음. 더 쉬운 방법이 있지만 이게 기초.
- 첫 번째 argument는 root에 들어갈 HTML tag.
- 두 번째 argument는 props가 포함된 object.
- 두 번쨰 argument는 'on'으로 시작하는 유효한 event가 있어야 함. (very powerful!)
- 세 번째 argument는 content.
