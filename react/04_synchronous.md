# 04_synchronous


## 동기/비동기 작업

- 동기 작업 : 하나의 작업을 실행하면 그게 끝난 후에 다음 작업을 순차적으로 처리하는 방법
- 비동기 작업 : 메인 흐름은 멈추지 않은 상태에서 특정 작업들을 백그라운드에서 동시에 처리하는 방법
    - 비동기 작업에서 가장 많이 사용되는 방식은 콜백 함수를 이용하는 것

## 콜백 지옥

- 비동기 API 사용시 비동기 처리 이후에 동작해야 하는 내용을 정의하는 경우 콜백함수의 중첩을많이 사용했는데, 이런 콜백함수의 중첩이 많아지면 가독성과 유지보수에 악영향을 주는데, 이를 콜백 지옥이라 한다.

## Promise

- ES6에서 콜백 지옥같은 코드가 형성되는 것을 막기 위한 방안으로 도입된 문법
- 현재 시점에서 ES6를 지원하지 않는 브라우저는 없기 때문에 별도로 babel이 필요하지 않음
- Promise는 일종의 객체라서, 동작시켜야 하는 콜백 함수를 Promise안에 넣음으로서 시작한다.
- Promise의 인자로는 (resolve, reject) 두가지로, resolve는 성공, reject는 실패를 의미한다.
    
    ```jsx
    // 입력받는 number에서 부터 10씩 더하는 콜백 함수. 그런데 결과가 50을 넘어가면 에러가 뜨는
    function increse(number) {
    	const promise = new Promise( (resolve, reject) => {
    	  setTimeout( () => {
    				const result = number + 10;
    	
    				if(result > 50){
    					const e = new Error('Number is big');
    	
    					return reject(e);  // 필수 아님
    				}
    	
    				resolve(result);
    			}, 1000
    		);
    	}); 
    
    	return promise;
    }
    ```
    
    - reject값은 반드시 설정해야 하는 것은 아니다.
    - return값은 Promise 객체러, 아래의 프로퍼티를 가진다.
        
        > [[Prototype]] : Promise
          [[PromiseState]] : "fulfilled"
          [[PromiseResult]] : 10
        > 
    - [[ ]] 대괄호 2개는 읽기 전용 데이터를 의미하며, 수정이 불가능하다.
    - [[PromiseResult]]는 직접 접근도 불가능하다.
    - 실행 결과를 출력하기 위해선 .then( ( ) ⇒ { } )을 사용해야 한다.
        
        ```jsx
        increase(0).then(number => {console.log(number)});
        
        increase(40).then(number => {
        	return increase(number);
        })
        .then(number => {  
        	return increase(number);    // return을 통해 then에서 사용했던 변수를 제공할 수 있다.
        })
        .catch( e => {
        	console.log(e);
        });
        ```
        
        - then( )은 실행 결과를 담고 있는 프로미스 객체라서 then()에 추가로 then()을 사용하는 게 가능하다
        - .catch를 통해서 에러값으로 설정한 reject의 결과도 반환받을 수 있다.(위 경우 reject 값을 에러로 설정했기에 .catch를 씀)

## async & await

- promise를 더 쉽게 사용할 수 있게 ES8(ES2017)에서 추가된 문법이다.
    
    ```jsx
    // Promise의 increase 함수를 똑같이 사용
    
    async function run() {
    	try{
    
    		let result = await increase(0);
    		console.log(result);
    
    		result = await increase(result);
    		console.log(result);
    
    		result = await increase(result);
    		console.log(result);
    
    		result = await increase(result);
    		console.log(result);
    
    		result = await increase(result);
    		console.log(result);
    
    		result = await increase(result);
    		console.log(result);
    
    	} catch(e) {
    		console.log(e);
    	}
    }
    ```
    
- 순차 계산을 해야하는 함수 앞에 await 키워드를 사용하면 됨
- await 키워드를 사용하려는 함수에는 async 키워드를 명시 해야 한다.
    
    > async : 비동기 방식을 동기 방식 흐름으로 실행시키겠다는 의미
    await : 값을 반환할 때 까지 기다리겠다
    >