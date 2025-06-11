
# Generic

## 📌 학습 내용 요약
***
# Generic이란
- 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법
- <> (꺽쇠괄호 or 다이아몬드 연산자)로 표현한다.
- List<String> list = new ArrayList<>();
- Reference 타입만 할당할 수 있다. (primitive 타입 불가능)

# 장점
- 컴파일 타임에 타입 검사를 통해 예외 방지
- 불필요한 캐스팅을 없애 성능 향상

# 주의 사항
1. 제네픽 타입의 객체는 생성 불가
   - 제네릭 타입으로는 인스턴스 생성이 불가 (T t = new T();)
2. static 맴버에 제네릭 타입이 올 수 없음.
   - public static T test(int a) {} -> X
3. 배열 선언 주의
   - 제네릭 클래스 자체를 배열로 생성할 수 없다.
     - Test<Integer>[] array = new Test<>[10]; -> X
   - 제네릭 타입의 배열을 선언할 수는 있다.
     - Test<Integer> array2 = new Test<>(); -> O 

# 타입 한정
1. 상위 타입 제한
   - <T extends [제한타입]>
   - <? extends [제한타입]>
2. 하위 타입 제한
   - <? super [제한타입]>
   - Bound Type 파라미터는 하위타입 제한 불가능
   - 와일드 카드 타입은 제네릭 타입의 인스턴스를 사용하는 시점에 제한하고, 바운드 타입(T)는 선언하는 시점에 제한하기 때문에
     하위 타입 제한은 사용이 불가능하다.
3. 다중 타입 제한
   - <T extends [제한타입(Class)] & [제한타입(Interface)] & ~~
4. 재귀적 타입 제한
   - <E extends Comparable<E>> : Comparable을 구현한 객체 이면서 E인 타입

# 타입 소거
1. 제네릭은 JDK1.5 이후부터 도입된 문법으로, 이전 자바에서는 제네릭 타입 파라미터 없이 사용했기 때문에 이전 버전의 자바 호환성을 위해 코드가 컴파일이 되고나면 제네릭 타입은 사라진다.
2. Process
   - 제네릭 타입의 경계(bound)를 제거한다.
     - <T extends Number> 일떄, 하위의 T는 Number로 치환된다.
     - <T>는 Object로 대체된다.
   - 제네릭 타입이 제거된 후 타입이 일치하지 않는 곳은 형변환이 추가된다.
3. Bridge 메서드
   - 컴파일러는 확장된 제네릭 타입에 대해 타입소거를 해도 다형성을 보존하기 위해 별도의 bridge 베서드를 생성한다.
   - 아래 코드에서 ClassCast 예외가 발생하는 이유가 Bridge Method가 생성되기 때문.
'''
class Generic<E> {
    public E element;

    public Generic(E element) {
        this.element = element;
    }

    public void setElement(E element) {
        this.element = element;
    }
}

class GenericChild extends Generic<Integer> {

    public GenericChild(Integer element) {
        super(element);
    }

    @Override
    public void setElement(Integer element) {
        this.element = element;
    }
}

class GenericTest {
    public static void main(String[] args) {
        GenericChild child = new GenericChild(10);

        Generic parent = child;
        parent.setElement("hello");
    }
}
'''



## 💡 느낀 점


## ❓ 궁금한 점


## 🔗 참고 링크
- 
