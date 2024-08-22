# 스택 (Stack)

### LIFO
Stack은 **LIFO**라는 특성을 가지는 데이터 구조 입니다.  
LIFO는 후입선출(Last In First Out)이라고 하는데, 가장 최근에 들어온 것이 제일 먼저 나가야 한다는 뜻입니다.  
  
우리 실생활에서 예시를 들어봅시다.
![접시 사진](이미지/stack_example.png)  
접시가 사진처럼 쌓여있을 때 중간에 있는 접시를 꺼내고 싶다면  
오른쪽 사진처럼 위쪽에 있는 접시(꺼내려는 접시보다 나중에 쌓여진 접시)를 꺼낸 후 중간에 있는 접시를 꺼낼 수 있습니다.  

스택 자료 구조도 마찬가지로 가장 최근에 들어온 데이터가 가장 먼저 나가야하는 구조로 이루어져 있습니다.  
  
<br>

### 작동
![스택 작동](이미지/stack_operation.png)  
<span style='font-size:11px'>(이미지 출처 : geeksforgeeks.org)</span>  

스택의 추상자료형(Abstract Data Type - ADT)를 보면 입력연산은 **Push**, 출력연산은 **Pop**이라고 합니다.  
그리고 조회연산은 **Peek**라고 하는데, **Top 포인터**가 가리키는 데이터를 확인만하고 Top의 인덱스는 변화시키지 않는 연산입니다.  
  
<br>

## 스택의 구현
Java에서는 기본적으로 Stack 클래스가 제공되지만, 직접 구현을 하고싶다면 보통 LinkedList를 사용합니다.

1. Stack
```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        // 스택에 값 추가
        stack.push(10);
        stack.push(20);
        stack.push(30);

        // 스택의 최상단 값 확인
        System.out.println("최상단 값: " + stack.peek());  // 30

        // 스택에서 값 꺼내기
        System.out.println("최상단 값: " + stack.pop());  // 30
        System.out.println("pop후에 최상단 값: " + stack.peek());  // 20

        // 스택이 비어있는지 확인
        System.out.println(stack.isEmpty());  // false
    }
}
```

2. LinkedList
```java
import java.util.LinkedList;

class CustomStack<T> {
    private LinkedList<T> list = new LinkedList<>();

    // 스택에 값 추가
    public void push(T value) {
        list.addFirst(value);
    }

    // 스택에서 값 꺼내기
    public T pop() {
        // 스택에 값이 있는지 확인 후 데이터 반환
        if (!isEmpty()) {
            return list.removeFirst();
        }
        return null;
    }

    // 스택의 최상단 값 확인
    public T peek() {
        // 스택에 값이 있는지 확인 후 데이터 반환
        if (!isEmpty()) {
            return list.getFirst();
        }
        return null;
    }

    // 스택이 비어있는지 확인
    public boolean isEmpty() {
        return list.isEmpty();
    }

    // 스택의 크기 확인
    public int size() {
        return list.size();
    }
}

public class StackExample {
    public static void main(String[] args) {
        CustomStack<Integer> stack = new CustomStack<>();

        // 스택에 값 추가
        stack.push(10);
        stack.push(20);
        stack.push(30);

        // 스택의 최상단 값 확인
        System.out.println("최상단 값: " + stack.peek()); // 30

        // 스택에서 값 꺼내기
        System.out.println("최상단 값: " + stack.pop()); // 30
        System.out.println("pop후에 최상단 값: " + stack.peek()); // 20

        // 스택이 비어있는지 확인
        System.out.println(stack.isEmpty()); // false
    }
}
```