# hook - useEffect

# Hook

> 리액트 16.8에서 새로 도입된 기능.
> 

> 함수형 컴포넌트에서 사용 불가능한 생명주기 메소드의 한계점으로 인해 상태관리 및 랜더링 이후 시점 컨트롤 등 다양한 문제를 해결하기 위해 만든 함수의 집합을 의미한다.
> 

> useState는 가장 기본적인 hook이며, 함수 컴포넌트에서도 상태(State)를 관리할 수 있게 해줌.
> 

> 컴포넌트가 랜더링 된 이후, 특정 작업을 수행할 필요가 있다면 클래스형 컴포넌트에서는 componentDidMount 또는 componentDidUpdate 메소드를 이용한다. 하지만 함수형 컴포넌트에서는 생명주기 api를 사용할 수 없다. 그렇기에 함수형 컴포넌트에서도 랜더링 이후 수행할 내용이 필요한 경우 사용할 수 있는 기능을 hook로 제공하고 있는데, 그것이 바로 useEffect이다.
> 

```jsx
const {useState, useEffect} = React;

function TimePrinter() {

	const [time, setTime] = useState( new Date().toLocaleTimeString() );

	useEffect(
		() => console.log('useEffect 작동');
	);

	return (
		<>
			<button onClick{ () => setTime( new Date().toLocaleTimeString() ) }>
				현재 시간 확인
			</button>
			<h1>{time}</h1>
		</>
	);
}

ReactDOM.createRoot(document.getElementById('root')).render(<TimePrinter/>);
```

- useEffect
    
    ```jsx
    // clean-up 없음
    useEffect( 
    	() => { 내용 }    // 함수
    , [...]             // 의존성 배열. 안써도 됨
    )
    ```
    
    - 컴포넌트 내부에서 선언하는 이유 : effect를 통해 const state 변수를 포함한 prop에 접근 할 수 있기 때문.
    - 함수부에는 보통 화살표함수로 선언된다. ( ) ⇒ { … }
    - 의존성 배열은 선언하게 될 경우, react동작시 의존성 배열 내에 선언된 요소가 업데이트 될 경우에만 useEffect가 동작하도록 설정할 수 있다. (선언하지 않을 경우 매 요소의 업데이트시마다 동작한다)
    - 의존성 배열 자리에 빈 배열( [] )을 선언할 경우, useEffect는 리액트가 실행된 후 최초의 랜더링 시에만 동작하게 된다.(반응할 요소가 없기 때문)
    
    ```jsx
    // clean-up
    useEffect(
    	() => { 내용 return () => { 리턴문 } }
    	, [...]
    )
    ```
    
    - 정리(clean-up)은 함수부의 실행 내역을 정리하여 보통 리액트의 성능을 끌어올리는 경우에 많이 사용한다.
    - 정리가 필요한 경우 함수를 반환하고, 그렇지 않은 경우는 아무것도 반환하지 않는다.