## 📌 학습 내용 요약
- Generic이 필요한 이유
    - **코드 재사용 (중복의 제거) & 타입 안정성**
- `<T>`: 타입 매개변수
- 객체를 생성하는 시점에 원하는 타입을 지정할 수 있다.
    
    ```java
    GenericBox<Integer> integerBox = new GenericBox<Integer>(); //Integer 타입만 허용 (여기서 Integer는 타입 인자라고 부름)
    GenericBox<Integer> integerBox2 = new GenericBox<>() // 타입 추론
    ```
    
    - 실제로 코드가 만들어지는게 아니라, 입력한 타입정보를 기반으로 이런 코드가 있다고 가정하고 컴파일 과정에 타입 정보를 반영한다.
- 클래스 내부에서 사용하는 타입을 클래스를 정의하는 시점이 아닌, 생성시점에 결정한다.
- 타입 인자로 기본형은 사용할 수 없다. (int, double, ..), Wrapper 클래스를 사용하면 된다.   
  (컴파일시 타입소거에 의해 내부적으로 Object 타입으로 처리되기 때문에..
- Raw type (원시 타입): <>를 지정하지 않는것
    
    ```java
    GenericBox integerBox = new GenericBox();
    ```
    
    - 자바의 제네릭은 자바가 처음 등장할때부터 있었던 것이 아니라서 제네릭이 없던 시절의 과거 코드와 호환이 필요하여 raw type을 지원한다. 되도록 사용해야하는 타입을 지정해서 사용하자.
    (Raw type을 사용하면 명시적인 형변환이 필요하고, 잘못된 타입의 객체를 저장하거나 꺼낼수 있기 때문에)
- 타입 매개변수 제한
    - `<T extends Animal>` : Animal 과 그 자식들만 받을 수 있도록 제한한다. T의 상한의 Animal
    - 타입 안정성을 지키면서, 상위 타입의 원하는 기능을 사용할 수 있어서, 코드 재사용성과 타입안정성을 지킬 수 있다.
- 제네릭 타입: `GenericClass<T>`, 객체를 생성하는 시점에 타입인자를 전달한다.
- 제네릭 메서드: `<T> T genericMethod(T t)`: 메서드를 호출하는 시점에 타입인자를 전달한다.
    - 예: `GenericClass.<Integer>genericMethod(i)`  (타입추론 가능)
- 참고
    - 제네릭 타입은 static 메서드에 타입 매개변수를 사용할 수 없다. 제네릭 타입은 객체를 생성하는 시점에 타입이 정해진다. 그런데 static 메서드는 인스턴스 단위가 아니라 클래스 단위로 작동하기 때문에 제네릭 타입과는 무관하다. 따라서 static 메서드에 제네릭을 도입하려면 제네릭 메서드를 사용해야 한다.
        
        ```java
        class Box<T> {
          T instanceMethod(T t) {} //가능
          static T staticMethod1(T t) {} //제네릭 타입의 T 사용 불가능
        }
        ```
        
- 제네릭 타입과 제네릭 메서드 우선순위
    - 제네릭타입보다 제네릭 메서드가 높은 우선순위를 가진다. 만약 이름이 겹친다면 둘 중 하나를 다른 이름으로 수정하자.
- 와일드 카드: `?`
- 상한 와일드 카드:  `<? extends Animal>` animal 이하의 타입만 들어올수있다.
- 하한 와일드 카드: `<? super Animal>` 하한이 animal, animal 혹은 더 상위 타입만 들어올 수 있다.
- **타입 이레이저:** 제네릭은 자바 컴파일 단계에서만 사용되고, 이후에는 제네릭 정보가 삭제된다. 제네릭에 사용한 타입 매개변수가 모두 사라진다. 컴파일 전인 .java 에는 제네릭 타입의 매개변수가 존재하지만, 컴파일 후인 바이트코드 .class 에는 타입 매개변수가 존재하지 않는다.
    
    예시
    
    1. 제네릭 타입 선언
        
        ```java
        public class GenericBox<T> {
          private T value;
          public void set(T value) {
            this.value = value;
          }
          public T get() {
            return value;
          }
        }
        ```
        
    2. Integer 타입인자로 전달
        
        ```java
        void main() {
          GenericBox<Integer> box = new GenericBox<Integer>();
          box.set(10);
          Integer result = box.get();
        }
        ```
        
    3. 자바 컴파일러는 GenericBox<Integer>() 에 대해 다음처럼 이해함.
        
        ```java
        public class GenericBox<Integer> {
          private Integer value;
          public void set(Integer value) {
        	  this.value = value;
          }
          public Integer get() {
        	  return value;
          }
        }
        ```
        
    4. 컴파일이 모두 끝나고 나면 제네릭과 관련된 정보를 삭제하는데 이때 .class 에 생성된 정보는 아래와 같다.
    (상한 제한 없이 선언한 타입 매개변수는 T를 Object로 변환한다.)
        
        ```java
        public class GenericBox {
          private Object value;
          public void set(Object value) {
        	  this.value = value;
          }
          public Object get() {
        	  return value;
          }
        }
        ```
        
        ```java
        void main() {
          GenericBox box = new GenericBox();
          box.set(10);
          Integer result = (Integer) box.get(); //컴파일러가 캐스팅 추가
        }
        ```
        
    - 자바의 제네릭 타입은 컴파일 시점에만 존재하고, 런타임 시에는 제네릭 정보가 지워지는데, 이것을 타입 이레이저라 한다.
    - 개발자가 직접 캐스팅하는 코드를 컴파일러가 대신 처리를 해주는 것이다. 컴파일 시점에 제네릭을 사용한 코드에 문제가 없는지 완벽히 검증하기 때문에 자바 컴파일러가 추가하는 다운캐스팅에는 문제가 발생하지 않는다.
    - 타입 이레이저 방식의 한계
        
        ```java
        class EraserBox<T> {
          public boolean instanceCheck(Object param) {
            return param instanceof T; // 오류 (항상 Object하고만 비교하게 되고, 항상 참임;)
          }
        
          public T create() {
            return new T(); // 오류 (항상 Object만 리턴하게 됨;)
          }
        }
        ```
        
        - `instanceOf`, `new` 를 허용하지 않는다

## 💡 느낀 점

## ❓ 궁금한 점

## 🔗 참고 링크
- [https://opentutorials.org/course/1223/6237](https://opentutorials.org/course/1223/6237)
- [https://dev-meung.tistory.com/entry/김영한의-실전-자바-중급-2편-1-제네릭-Generic](https://dev-meung.tistory.com/entry/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-2%ED%8E%B8-1-%EC%A0%9C%EB%84%A4%EB%A6%AD-Generic)
