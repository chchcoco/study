# 화살표 함수


- function 키워드 대신 화살표를 사용하여 더 간략하게 함수를 선언하는 방법
- 화살표 함수로 정의하는 것은 항상 익명 함수
- 한 줄 짜리 함수 작성 시 더 유용

```jsx
let func1;

// 기존 function
func1 = function () {
	return "hello world";
};

// 화살표 함수
func1 = () => {
	return "hello world";
};

// 본문이 한 줄 일 경우 중괄호 생략 가능
// return 키워드 생략 가능
func1 = () => "hello world";

// 매개변수가 있는 경우
func1 = (var1, var2) => "Hello" + var1 + ", " + var2;

// 매개변수가 하나인 경우에만 소괄호 생략가능
func1 = var1 => "Hello" + var1;

// 리턴이 객체 리터럴일 경우 소괄호를 감싼다.
// 소괄호로 감싸지 않으면 함수부를 의미하는 중괄호로 잘못 해석함
const user = (id, name) => ({id, name});

// 고차 함수에 인수로 전달 가능 -> 일반 함수 표현보다 간결
console.log([1, 2, 3].map(function(val){ return val * 10 }));
console.log([1, 2, 3].map(val => val * 10));

```

### 화살표 함수의 특징

- 화살표 함수는 표현 뿐만 아니라 내부 동작도 간략화 되어있다.
- 일반 함수와의 차이점
    1. 화살표 함수는 this를 가지지 않음
        
        객체의 메소드 안에서 동일한 객체의 프로퍼티를 대상으로 순회하는 데에 사용가능
        
        ```jsx
        let alphabet = {
        	nation: "USA",
        	alpha: ["a", "b", "c", "d", "e"],
        
        	showList() {
        		this.alpha.forEach(    // 화살표 함수 본문에서 this 접근시, 외부에서 값을 가져옴 -> this.alpha는 alphabet.alpha를 의미
        			alpha => console.log(this.nation + ':' + alpha)
        		);
        	}
        }
        ```
        
    2. 화살표 함수는 new와 함께 호출 불가능
        
        this가 없음 → 생성자 함수 사용 불가 = 인스턴스 생성 못함 = prototype 프로퍼티 없음 & 프로토타입 생성 불가
        
        ```jsx
        const method2 = () => {};
        // new method2();는 에러발생 : TypeError - constructor없음
        ```
        
    3. super 없음
        
        super 지원 안함 → 화살표 함수 내에서 super 사용시 외부에서 가져옴 → 외부의 요소 가져오기가 가능
        
    4. arguments 지원 안함
        
        ```jsx
        (function(){
        	const arrowFunction = () => console(arguments);
        	arrowFunction(1, 2);
        }(3, 4));	
        ```
        
        - 화살표 함수의 arguments : 1, 2가 아닌 상위 스코프의 arguments 3, 4로 참조됨.