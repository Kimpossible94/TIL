# 문자열 내 p와 y의 개수
## 문제 설명
대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True,  
다르면 False를 return 하는 solution를 완성하세요.  
'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다.  
단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.  

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

## 제한 조건
* 문자열 s의 길이 : 50 이하의 자연수
* 문자열 s는 알파벳으로만 이루어져 있습니다.

## 풀이
### 나의 풀이
```java
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        
        int numP = 0;
        int numY = 0;
        
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            
            if(c == 'y' || c == 'Y') numY++;
            else if (c == 'p' || c == 'P') numP++;
        }
        
        if(numP != numY) answer = false;

        return answer;
    }
}
```  

## 다른 사람의 풀이
```java
class Solution {
    boolean solution(String s) {
        s = s.toLowerCase();
        int count = 0;

        for (int i = 0; i < s.length(); i++) {

            if (s.charAt(i) == 'p')
                count++;
            else if (s.charAt(i) == 'y')
                count--;
        }

        if (count == 0)
            return true;
        else
            return false;
    }
}
```
count라는 변수 하나만을 써서 문제를 해결했다.  
p가 나올 때 더하고, y가 나올 때 마이너스를 해서 0이라면 p와 y의 숫자가 같거나 나오지 않은 것이므로 true를 리턴하고,  
다르다면 포함횟수가 다른것이므로 false를 리턴하도록 하였다.

```java
class Solution {
    boolean solution(String s) {
        s = s.toUpperCase();

        return s.chars().filter( e -> 'P'== e).count() == s.chars().filter( e -> 'Y'== e).count();
    }
}
```
스트림을 통해서 문제를 해결했다.  
chars()는 문자열을 구성하고는 있는 문자들의 ASCII코드 값을 스트림 형태로 뽑아준다.  
```java
IntStream stream = "Hello,World".chars(); //(72, 101, 108, 108, 111, 44, 87, 111, 114, 108, 100)
```
그리고 filter()로 조건에 맞는 요소만 뽑은 후 count()로 요소 수를 반환해 비교하는 방식으로 문제를 해결했다.



#### 다른 사람의 문제풀이를 보니 문자열을 미리 toUpperCase()를 이용해 바꿔놓는 것을 확인할 수 있다. 참고해야겠다.