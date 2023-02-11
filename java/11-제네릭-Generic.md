---
marp: true
---

제네릭(Generic)
===
- 데이터 타입을 일반화 하는 기능
- JDK 1.5에서 추가된 문법
- 데이터의 형식에 의존하지 않고 하나의 값이 여러 데이터 타입들을 가질 수 있게 하여 재사용성을 높이는 프로그래밍 방식
- 사용법
    > 다이아본드 연산자 내부에 T를 작성 : <T>   //여기서 T는 타입변수
    타입 변수를  자료형 대신에 사용. T(타입변수)는 가상의 타입.
    사용하는 쪽에선 타입변수 자리에 맞춰서 탕비을 넣으면, 컴파일 시점에 해당 타입으로 결정.

---
```
public class GenericClass<T> {
    public T var1;
}
```
```
public class App{
    public static void main(String[] args){
        GenericClass<Integer> gc1 = new GenericClass<Integer>();
        gc1.var1 = 1;

        GenerucClass<String> gc2 = new GenericClass<>();    //jdk 7에서 추가된 문법
        gc2.var1 = "Hello World";
    }
}
```
- jdk 7에서 타입변수 생성시 호출 구문쪽에서 타입 생략하고 사용가능.(타입 추론이 가능해서)
---
# 와일드 카드(WildCard)
- 제네릭 클래스 타입의 객체를 메소드의 매개변수로 받을 때, 그 객체의 타입변수를 제한하는 문법
  - <?> : 제한 없음
  - <? extends Type> : 와일드 카드 상한 제한 (Type || Type의 후손 타입만 사용 가능)
  - <? super Type> : 와일드 카드 하한 제한 (Type || Type의 부모 타입만 사용 가능 )

---
```
/* Generic Class */
public class PrintChar<T extends Alphabet>{

    public void printAlpha(T alpha){
        System.out.println(T);
    }

}
```

```
/* Wild Card */
public class PrintChar{
    
    public void printAlpha(PrintChar<? extends LargeAlpha> pc){
        pc.printAlpha();
    }
}
```