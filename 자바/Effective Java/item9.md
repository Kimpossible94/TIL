# Item 9. try-finally보다는 try-with-resources를 사용하라

## 자원회수
자바 라이브러리에는 close 메서드를 사용해서 회수해줘야 하는 자원이 많다.  
자원 회수를 놓치면 예상할 수 없는 성능문제로 이어질 수 있기 때문에 자원을 반드시 회수하는게 좋다.  

이런 자원 회수를 위해 전통적으로 try-finally이 쓰였다.  
하지만 이는 자원을 회수하는데 최선책은 아니다.  

## try-finally 예시
```java
static String firstLineOfFile(String path) throws IOException {
   BufferedReader br = new BufferedReader(new FileReader(path));
   try {
      return br.readLine();
   } finally {
      br.close();
   }
}
```  
전통적으로 상기의 코드처럼 사용했다.  
여기에는 미묘한 결점이 있다.  
try문과 finally문 모두에서 예외가 발생했다고 가정해보자.  
br.readLine()에서 발생한 예외는 close()에서 발생한 예외에게 잡아먹힐 것 이다.  
이렇게 된다면 스택 추척 내역에 첫번째 예외에 대한 내역이 남지않아 디버깅을 어렵게할 것 이다.  

  
두번째 예시를 보자
```java
static void copy(String src, String dst) throws IOException {
   InputStream in = new FileInputSystem(src);
   try {
      OutputStream out = new FileOutputStream(dst);
      try {
         byte[] buf = new byte[BUFFER_SIZE];
         int n;
         while ((n = in.read(buf)) >= 0) {
            out.write(buf, 0, n);
         }
      } finally {
         out.close();
      }
   } finally {
      in.close();
   }
}
```
상기의 예시는 회수해야 하는 자원이 2개 이상일 때의 예시이다.  
첫번 째 예시와 똑같은 문제가 발생할 수 있는건 마찬가지이고 코드가 너무 지저분해진다.  

## try-with-resources
이러한 문제는 자바7 부터 도입된 try-with-resources덕에 모두 해결되었다.  
이 구조를 사용하려면 해당 자원이 AutoCloseable 인터페이스를 구현해야한다.
AutoCloseable 인터페이스는 단순히 void를 반환하는 close 메서드 하나만 덩그러니 정의한 인터페이스이다.  

![alt text](이미지/AutoCloseable.png)
(https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/AutoCloseable.html)  

이제 try-with-resources로 앞선 2개의 예시를 재작성해보면 아래와 같다.  
```java
static String firstLineOfFile(String path) throws IOException {
   try (BufferedReader br = new BufferedReader(new FileReader(path))) {
      return br.readLine();
   }
}
```  

```java
static void copy(String src, String dst) throws IOException {
   try(InputStream in = new FileInputSystem(src);
   OutputStream out = new FileOutputStream(dst)) {
      byte[] buf = new byte[BUFFER_SIZE];
      int n;
      while ((n = in.read(buf)) >= 0) {
         out.write(buf, 0, n);
      }
   }
}
```  
앞에서 말한 문제점들이 해결된 것을 볼 수 있다.  
일단 코드가 간결해져 가독성이 매우 올라갔고, br.readLine()과 close() 모두에서 예외가 발생했을 때 readLine()에서 발생한 예외가 기록된다.  
close()에서 발생한 예외도 버려지지않고 스택 추적 내역에서 "숨겨졌다(suppressed)"라는 꼬리표를 달고 출력된다.

## 결론
꼭 회수해야 하는 자원을 다룰 때는 try-finally 말고 try-with-resources를 사용하자.  
예외는 없으니 무조건 try-with-resources를 사용하는 것이 옳다.