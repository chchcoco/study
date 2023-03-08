# Iterable

> ES6 이전의 순회 가능한 데이터 컬렉션, 배열, 문자열, 유사 배열 객체, DOM 컬랙션 등은 통일된 규약 없이 for문, for…in문, forEach 메소드 등 다양한 방법으로 순회 가능
> 

> ES6에서는 순회 가능한 데이터 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일하여 for…of문, 스프레드 문법, 배열 디스트럭쳐링 할당의 대상으로 사용할 수 있도록 일원화 함
> 
- 이터러블(iterable)은 Symbol.iterator가 구현된 객체
    
    ```jsx
    let range = {
    	from: 1,
    	to: 5
    };
    
    range[Symbol.iterator] = function() {
    	return{
    		current: this.from,
    		last: this.to,
    
    		next() {
    			if(this.current <= this.last){
    				return { done: false, value: this.current++};
    			} else {
    				return { done: true };
    			}
    		}
    	};
    };
    
    for(let num of range) {
    	console.log(num);
    }
    ```
    
    - Symbol.iterator를 추가.  for..of 최초 호출 시, Symbol.iterator가 호출됨
    - Symbol.iterator는 이터레이터 객체를 반환함
    - for..of 반복문에 의해 반복마다 next() 호출, next()는 값을 { done: ..., value: … } 객체 형태로 반환
    - done은 반복이 끝났음을 의미, 끝나지 않은 경우 value가 다음 값이 됨
    - 객체 선언 후 for..of 반복문 호출시 오류(range is not iterable)
    -