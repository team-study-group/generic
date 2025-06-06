**gemini 문제 생성**

*Pair 클래스 만들기*
***
```
public class Problem1 {
    public static void main(String[] args) {
        // String과 Integer 쌍
        Pair<String, Integer> stringIntPair = new Pair<>("Hello", 123);
        System.out.println("String-Integer Pair: (" + stringIntPair.getFirst() + ", " + stringIntPair.getSecond() + ")");

        // Integer와 Integer 쌍 (Comparable 가능)
        Pair<Integer, Integer> intPair = new Pair<>(50, 30);
        System.out.println("Integer Pair: (" + intPair.getFirst() + ", " + intPair.getSecond() + ")");
        System.out.println("Min Value: " + intPair.getMinValue());
        System.out.println("Max Value: " + intPair.getMaxValue());

        // Double과 Double 쌍 (Comparable 가능)
        Pair<Double, Double> doublePair = new Pair<>(3.14, 2.71);
        System.out.println("Double Pair: (" + doublePair.getFirst() + ", " + doublePair.getSecond() + ")");
        System.out.println("Min Value: " + doublePair.getMinValue());
        System.println("Max Value: " + doublePair.getMaxValue());

        // String과 String 쌍 (Comparable 가능)
        Pair<String, String> stringPair = new Pair<>("banana", "apple");
        System.out.println("String Pair: (" + stringPair.getFirst() + ", " + stringPair.getSecond() + ")");
        System.out.println("Min Value: " + stringPair.getMinValue());
        System.out.println("Max Value: " + stringPair.getMaxValue());

        // String과 Integer 쌍에서 getMinValue/getMaxValue 호출 시 컴파일 에러 발생 확인 (테스트 코드)
        // Pair<String, Integer> compileErrorPair = new Pair<>("test", 1);
        // compileErrorPair.getMinValue(); // 컴파일 에러 발생해야 함
    }
}
```

*ListProcessor 클래스 만들기*
***
```
import java.util.ArrayList;
import java.util.List;

// main 메서드 (수정 불가)
public class Problem2 {
    public static void main(String[] args) {
        List<Integer> integers = new ArrayList<>();
        integers.add(1);
        integers.add(2);

        List<Double> doubles = new ArrayList<>();
        doubles.add(3.14);
        doubles.add(2.71);

        List<Number> numbers = new ArrayList<>(); // Integer, Double의 부모
        List<Object> objects = new ArrayList<>();   // 모든 것의 부모

        // copyList 테스트
        System.out.println("--- Copying Integers to Numbers ---");
        ListProcessor.copyList(integers, numbers); // Integer -> Number (Extends, Super)
        ListProcessor.printAll(numbers); // 1, 2 출력

        System.out.println("--- Copying Doubles to Objects ---");
        ListProcessor.copyList(doubles, objects); // Double -> Object (Extends, Super)
        ListProcessor.printAll(objects); // 3.14, 2.71 출력

        System.out.println("--- Copying Numbers to Objects ---");
        ListProcessor.copyList(numbers, objects); // Number -> Object (Extends, Super)
        ListProcessor.printAll(objects); // 1, 2, 3.14, 2.71 출력 (기존 내용 유지)

        // printAll 테스트
        System.out.println("--- Printing various lists ---");
        ListProcessor.printAll(integers); // 1, 2 출력
        ListProcessor.printAll(doubles);  // 3.14, 2.71 출력
        ListProcessor.printAll(numbers);  // 1, 2 출력 (이전 내용 유지)
        ListProcessor.printAll(objects);  // 1, 2, 3.14, 2.71 출력 (이전 내용 유지)

        // 컴파일 에러가 나야 하는 경우 (테스트 코드)
        // ListProcessor.copyList(numbers, integers); // 컴파일 에러: Number를 Integer 리스트에 넣을 수 없음
        // ListProcessor.copyList(objects, doubles);  // 컴파일 에러: Object를 Double 리스트에 넣을 수 없음
    }
}
```


*Util 클래스 만들기*
***
```
import java.io.Serializable;
import java.util.ArrayList;
import java.util.List;

// main 메서드 (수정 불가)
public class Problem3 {
    public static void main(String[] args) {
        MyRunnableCloneableSerializable obj1 = new MyRunnableCloneableSerializable("Task 1");
        Util.printInfo(obj1);

        System.out.println("---");

        MyRunnableCloneableSerializable obj2 = new MyRunnableCloneableSerializable("Task 2");
        Util.printInfo(obj2);

        // 컴파일 에러가 나야 하는 경우 (테스트 코드)
        // class SimpleRunnable implements Runnable { public void run() { System.out.println("Simple"); } }
        // Util.printInfo(new SimpleRunnable()); // 컴파일 에러: Cloneable, Serializable 미구현
    }
}

// 다음 클래스는 수정하지 마세요. (문제의 제약을 충족하는 예시 클래스)
class MyRunnableCloneableSerializable implements Runnable, Cloneable, Serializable {
    private String name;

    public MyRunnableCloneableSerializable(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        System.out.println(name + " is running.");
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public String toString() {
        return "MyRunnableCloneableSerializable{" + "name='" + name + '\'' + '}';
    }
}
```

*Box, GiftBox 클래스 만들기*
***
```
public class Problem4 {
    public static void main(String[] args) {
        // Box<String> 생성
        Box<String> stringBox = new Box<>("Hello World");
        String content = stringBox.getItem();
        System.out.println("Box content: " + content);

        // GiftBox<Integer> 생성
        GiftBox<Integer> integerGiftBox = new GiftBox<>(12345);
        Integer giftContent = integerGiftBox.getItem(); // Box의 getItem 사용
        System.out.println("GiftBox getItem: " + giftContent);
        Integer unwrappedContent = integerGiftBox.unwrap(); // GiftBox의 unwrap 사용
        System.out.println("GiftBox unwrapped: " + unwrappedContent);

        // GiftBox<Double> 생성
        GiftBox<Double> doubleGiftBox = new GiftBox<>(987.65);
        Double unwrappedDouble = doubleGiftBox.unwrap();
        System.out.println("GiftBox unwrapped double: " + unwrappedDouble);

        // 컴파일 에러 발생 여부 확인 (테스트 코드)
        // GiftBox<Number> numberGiftBox = new GiftBox<>(100);
        // String test = numberGiftBox.unwrap(); // 컴파일 에러: Number를 String으로 변환 불가
    }
}

```

*Sorter, BubbleSorter (sort 구현까지는 x) 클래스 만들기*
***
```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

// main 메서드 (수정 불가)
public class Problem5 {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>(Arrays.asList(5, 2, 8, 1, 9, 4));
        System.out.println("Original Numbers: " + numbers);
        Sorter<Integer> intSorter = new BubbleSorter<>(Comparator.naturalOrder()); // 오름차순 정렬
        intSorter.sort(numbers);
        System.out.println("Sorted Numbers (Asc): " + numbers); // 1, 2, 4, 5, 8, 9

        List<String> names = new ArrayList<>(Arrays.asList("banana", "apple", "grape", "cherry"));
        System.out.println("Original Names: " + names);
        Sorter<String> stringSorter = new BubbleSorter<>(Comparator.reverseOrder()); // 내림차순 정렬
        stringSorter.sort(names);
        System.out.println("Sorted Names (Desc): " + names); // grape, cherry, banana, apple

        // 커스텀 객체 정렬 (Comparable을 구현하지 않아도 Comparator로 정렬 가능)
        class Person {
            String name;
            int age;

            public Person(String name, int age) {
                this.name = name;
                this.age = age;
            }

            @Override
            public String toString() {
                return name + "(" + age + ")";
            }
        }

        List<Person> people = new ArrayList<>(Arrays.asList(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Charlie", 35)
        ));
        System.out.println("Original People: " + people);

        // 나이 기준 오름차순 정렬
        Sorter<Person> personAgeSorter = new BubbleSorter<>(Comparator.comparingInt(p -> p.age));
        personAgeSorter.sort(people);
        System.out.println("Sorted People by Age (Asc): " + people); // Bob(25), Alice(30), Charlie(35)

        // 이름 기준 내림차순 정렬
        Sorter<Person> personNameSorter = new BubbleSorter<>(Comparator.comparing(p -> p.name, Comparator.reverseOrder()));
        personNameSorter.sort(people);
        System.out.println("Sorted People by Name (Desc): " + people); // Charlie(35), Bob(25), Alice(30)
    }
}
```


https://gemini.google.com/app/2f09178fdc208fa1?utm_source=chrome_omnibox&utm_medium=owned&utm_campaign=gemini_shortcut
