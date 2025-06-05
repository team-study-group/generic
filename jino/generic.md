# Generic

## 📌 학습 내용 요약
- 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법
  - 인스턴스 안에 데이터 타입
  - List<String> list = new ArrayList<>();
    - ArrayList<E> extends AbstractList<E>
    - Object 로 처리하다가 리턴 할 때는 (E) 로 형변환 처리 함
    - 값을 넣을 때는
      - add(E e) { 
          // array 한칸 늘려서 array copy 후
        Object[] elementData[index] = e;
      } 이런 느낌
- 

## 💡 느낀 점
- 

## ❓ 궁금한 점
- 

## 🔗 참고 링크
- 
