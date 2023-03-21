# 05_Router

### 라우터

- 요청이 들어온 경우, 라우팅 테이블을 기반으로 요청을 적절히 분산하는 장치

### 번들

- 여러 .js 파일들을 모아놓은 것
- 번들들을 모아주는 프로그램을 번들러라고 한다.

### index.html

- 웹팩이라는 번들러가 .js파일들을 모아 만들어 내는 html 파일.
- /index.html 이라는 페이지 주소는 웰컴 페이지라고도 하며, 브라우저가 이를 묵시적으로 선언하기에, 도메인만 있는 페이지는 사실 index.html 이 생략되어 있는 것이다.

### React Router

- 리액트 라우터는 JS core문법과 node.js 문법을 사용한다
- 리액트 라우터를 사용하기 위해서는 import해주어야 한다.
    
    ```jsx
    import { BrowserRouter, Routes, Route } from 'react-router-dom'
    ```
    
- 리액트 라우터 사용하기
    
    ```jsx
    <BrowserRouter>
    	<Routes>
    		<Route path='/' element={ <Layout/> }/>
    			<Route index element={ <Main/> }/>
    			<Route path='/about' element={ <About/> }/>
    			<Route path='/menu' element={ <Menu/> }/>
    		<Route/>
    	</Routes>
    </BrowserRouter>
    ```
    
    - <Route path=”/elem” element={<Element/>}/>
        - 해당 엘리먼트에 path에 선언된 url을 할당하며, 해당 url인 경우 다음의 element를 랜더 하겠다는 의미이다.
        - 특정 path의 Route 내부에 선언된 경우, 그 Route의 url뒤에 추가로 붙는다.
        - path가 아닌 index 라우팅의 경우, 해당 url에서 element를 랜더링하겠다는 의미이다.
        - React의 라우팅은 html 문서간 이동이 아니라 하나의 문서 내에서 컴포넌트들의 변화를 감지하여 render tree를 갱신하여 새로 랜더링 하는 방식이다.
    - 경우에 따라 <

## Navigating

- url이 바뀌는 것을 navigation이라 하며 react에는 url을 바꾸는 방법이 2가지가 있다.

### Link

- 링크 컴포넌트는 클릭시, 저장된 url로 이동한다.
- <a>태그와 다른 점은 <a>는 해당 url로 이동하며 페이지 자체를 새로 불러오는 반면, Link는 url만 이동한다.
    
    ### NavLink
    
    - 스타일을 추가할 수 있는 특별한 Link

### useNavigate

- 라우터가 지원하는 hook
    
    ```jsx
    import { useNavigate } = from 'react-router-dom';
    
    function Page() {
    	
    	const navigate = useNavigate();
    
    	
    }
    ```
    
    - url을 이동할 때 사용한다.

### Outlet

- 부모 Route의 element를 자식 Route의 element에 랜더시킬 때 사용하는 태그
- 랜더 시키고 싶은 부모 Route의 컴포넌트들 아래에 <Outlet/>를 선언하면 outlet 태그 위의 요소들은 자식 Route의 element를 랜더 할 때도 계속 남아있게 된다.