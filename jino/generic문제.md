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
