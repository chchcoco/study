---
marp: true
---

# 컬렉션 Collection - 컬렉션 프레임워크
> 데이터를 효율적으로 저장하는 자료구조와 데이터를 처리하는 알고리즘을 구현해 놓은 클래스
- List 인터페이스
    - 순서 있는 데이터 집합. 중복저장 허용
    - Vector ArrayList, LinkedList, Stack, Queue 등
- Set 인터페이스
    - 순서 없는 데이터 집합. 중복 미허용
    - HashSet, TreeSet 등
- Map 인터페이스
    - 키와 값 한 쌍으로 이뤄진 데이터 집합
    - key는 set 방식으로 관리 -> 데이터 순서 관리 안함 & 중복 미허용
    - value는 중복값 저장 가능
    - HashMap, TreeMap, HashTable Properties 등
---
ArrayList( implements List )
===
- JDK 1.2부터 제공
- 내부적으로 배열로 요소 관리, 인덱스를 통해 배열 요소에 접근
- 배열의 크기 고정, 요소의 추가/삭제/정렬 등이 복잡하다는 단접을 보완
- 크기 변경, 요소의 추가/삭제/정렬 기능을 미리 구현하고 제공
    (속도가 빨라지는 것은 아님)
---
ArrayList 선언
===
```
List list = new ArrayList();
```
- 다형성을 적용하여 상위타입으로 ArrayList 객체를 생성
- List의 하위 구현체들로 타입변경이 가능해져서 래퍼런스 타입을 List로 해두는 것이 더 유연한 코드 작성 가능

---
ArrayList 사용(1)
===
```
list.add(100);
list.add(True);
list.add(50.01);
list.add("HelloWorld");
list.add(new java.util.Date());
```
- .add()를 통해 ArrayList에 요소 추가 가능
```
for(int i = 0; i < list.size(); i++){
    System.out.println(i + " : " + list.get(i));
}
```
- .size()를 통해 값이 저장된 요소들의 수를 int로 얻을 수 있음
- .get(index)를 통해 해당 인덱스의 요소를 반환받을 수 있음
---
ArrayList 사용(2)
===
```
/* 해당 인덱스에 값을 추가하는 메소드
 * 해당 번째와 이후에 있던 요소들은 자동으로 뒤로 이동함
 */
list.add(1, "AAA");  

/* 해당  인덱스의 요소를 지우는 메소드 */
list.remove(2);

/* 해당 인덱스의 값을 입력한 값으로 변경하는 메소드 */
list.set(1, "Exchange");
```
---
ArrayList 사용(3) - 제네릭 타입 선언
===
```
List<String> strList = new ArrayList<>();
```
- 모든 컬렉션 프레임워크 클래스들은 제네릭 클래스로 작성됨
- <> 내부에 타입을 선언하여 원하는 안에 넣는 타입을 한정할 수 있음
- <>를 비우거나 안쓰는 경우 Object타입이 됨

---
ArrayList 사용(4) - 정렬
===
- .sort() 메소드를 이용하여 오름차순/내림차순 정렬이 가능
    1. Comparator 상속받아 compare(obj1, obj2) 오버라이딩
        > compare()는 sort()에서 내부적으로 사용하는 메소드.
        > 인자로 들어온 두 값을 비교하여 앞이 작으면 -1, 같으면 0, 뒤의 값이 작으면 1을 반환
        > compare()가 양수가 들어오면 sort()는 두 값의 위치를 바꿈 -> 오버라이딩을 통해 출력값을 반대로 하면 내림차순 정렬도 쌉가능
    2. 람다식 활용
        ``` list.sort((T obj1, T obj2) -> obj1.getValue() >= obj2.getValue() ? -1 : 1); ```
        - 람다식 : ( (인자 [, 인자, ...]) -> 실행문 )
        - 즉석으로 함수를 작성하는 문법으로 인자를 주면 인자를 갖고 실행하는 메소드를 즉석으로 작성하여 사용.

---
LinkedList
===

- ArraryList가 배열을 사용하므로 발생하는 성능적인 단점을 보완
- 내부는 이중 연결리스트로 구현
```
List<String> linkedList = new LinkedList<>();
```
- ArrayList와 같이 .add(), .get(), .remove() 등은 List 인터페이스를 상속하므로 동일하게 사용 (내부 로직은 다름)

---
Stack
===
- 리스트 계열의 클래스 Vector클래스를 상속받아 구현
- 후입선출(LIFO; Last In First Out) 방식의 자료구조

```
Stack<Integer> intStack = new Stack<>();

intStack.push(1);
intStack.push(2);
intStack.push(3);

System.out.println(intStack);
```
> 결과 :  [1, 2, 3]
- Stack에 값을 넣을 때는 push()를 이용


---
Iterator(반복자)
===
- Collection 인터페이스의 iterator() 메소드를 이용해 생성한 인스턴스
- 컬렉션에서 값을 읽어오는 방식을 통일된 방식으로 제공하기위해 사용
- 반복문을 이용해 목록을 하나씩 꺼내는 방식으로 사용
- 인덱스로 관리되는 컬렉션이 아닌경우 요소에 하나씩 접근하기 위한 통일된 방식을 제공
```
Iterator<String> iter = ((LinkedList<String>) strList).descendingIterator();
while(iter.hasNext()){                  // .hasNext() : 다음 요소가 있으면 true, 없으면 false를 반환하는 메소드
    System.out.println(iter.next());    // .next() : 다음 요소를 반환하는 메소드
}
```
- next로 접근한 Iterator는 다시 접근이 불가능하다
---
