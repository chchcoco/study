# State & useState

## state

> 컴포넌트 내부에서 바뀔 수 있는 값을 의미. props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값이지만, state는 컴포넌트 내부에서 결정되는 값.
> 
- props는 읽기 전용, state는 변경되는 값을 관리

- 클래스 컴포넌트의 생성자에서 state
    
    ```jsx
    class Counter extends React.Component {
    
    	constructor(props){
    		super(props);
    
    		this.state = {
    			var1 : 0
    		};
    	}
    
    	render() {
    		const {var1} = this.state;
    
    		return(
    			<>
    				<h1 style={(var1 < 0)? {color: 'red'}: {color: 'blue'}}>Var1: {var1}</h1>
    				<button onClick={() => this.setState({var1: var1 - 1})}>-1</button>
    				<button onClick={() => this.setState({var1: var1 + 1})}>+1</button>
    			</>
    		);
    	}
    }
    
    ReactDOM.createRoot(document.getElementById('root')).render(<Counter/>);
    ```
    
    - constructor(props)
        - 컴포넌트 생성 시 가장 먼저 호출되는 함수는 생성자 함수.
    - super(props)
        - 생성자 함수의 첫 문장은 부모 컴포넌트로부터 전달받은 props를 부모 클래스 생성자에게 전달하는 것
    - this.state :
        - state를 초기화
        - state는 생성자 내에서 초기화 하는 경우 this.을(를) 써야하며, 반드시 이름을 state로 해야한다.
        - state에 저장되는 값의 형태는 반드시 Object 리터럴 형태로 작성해야 한다.:  { 요소: 값 }

## prevState

- setState()
    - prevState()를 사용할 경우, 상태 변경이 일어나고 리랜더링이 되어야 state값 변경이 적용된다.
    - 하나의 EventHandler에서 여러번 setState를 호출한다해도 누적되어서 state가 갱신되지는 않는다.
    - 누적 처리를 해고 싶다면 변경할 state 객체 대신 함수를 전달하면 된다.
    - 전달하는 콜백함수의 첫번째 인자는 이전 상태값을 가리키는 prevState이며, 두번째 인자는 현재 갖고있는 props이다. props는 필요하지 않다면 생략할 수 있다.
    
    ```jsx
    class Counter extends React.Component {
    	state = { var1 : 0 };
    
    	render() {
    		const { var1 } = this.state;
    
    		return(
    			<>
    				<h1>Count : {number}</h1>
    				{/* <button>-1</button> */}
    				<button
    					onClick = {
    						() => {
    							this.setState( (prevState, props) => {
    									return{ var1 : prevState.var1 + 1 }
    								}
    							);
    							this.setState((prevState, props) => ({var1: prevState.var1 + 1}));
    						}
    					}
    				>
    					+1
    				</button>
    			</>
    		);
    	}
    }
    
    ReactDOM.createRoot(document.getElementById('root')).render(<Counter/>);
    ```
    

## useState

> useState는 React 객체 내부에 존재하는 함수형 프로퍼티이다. 따라서 React.useState() 의 형태로 호출하여 사용해야한다. 하지만 비구조화 할당을 통해 미리 전역변수로 선언해두면 React.를 생략하고 useState()로 사용할 수 있다.
> 

```jsx
const { useState } = React;

function ShowNum() {
	const [number, setNumber] = useState(0);
	const [color, setColor] = useState('black');
	const [backgroundColor, setBackgroundColor] = useState('white');

	const onClickPlus = () => setNumber(number + 1);
	const onClickMinus = () => setNUmber(numbser - 1);

	return(
		<>
			<h1 style={{color, backgroundColor}}>{number}</h1>
			<div>
				<button onClick={ onClickPlus }>+ 1</button>
				<button onClick={ onClickMinus }>- 1</button>
			</div>
			<div>
				<button onClick={ () => setColor('red') }>red</button>
				<button onClick={ () => setColor('blue') }>blue</button>
				<button onClick={ () => setColor('green') }>green</button>
			</div>
			<div>
				<button onClick={ () => setBackgroundColor('white') }>기본 배경</button>
				<button onClick={ () => setBackgroundColor('black') }>검은 배경</button>
			</div>
		</>
	);
}

ReactDOM.createRoot(document.getElementById('root')).render(<ShowNum/>);
```