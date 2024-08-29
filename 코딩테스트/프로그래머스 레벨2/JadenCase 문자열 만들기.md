# JadenCase 문자열 만들기
## 문제 설명
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

## 제한 조건
* s는 길이 1 이상 200 이하인 문자열입니다.
* s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
  * 숫자는 단어의 첫 문자로만 나옵니다.
  * 숫자로만 이루어진 단어는 없습니다.
  * 공백문자가 연속해서 나올 수 있습니다.

## 풀이
### 나의 풀이
```java
class Solution {
    public String solution(String s) {
        StringBuilder sb = new StringBuilder();
        String[] strings = s.toLowerCase().split(" ");

        for (String string : strings) {
            if(string.length() == 0) {
                sb.append(" ");
                continue;
            }

            sb.append(string.substring(0, 1).toUpperCase());
            sb.append(string.substring(1));
            sb.append(" ");
        }
        
        // 테스트케이스 8번 통과못해서 넣어줘야함.
        if(!" ".equals(s.substring(s.length()-1))) {
            sb.deleteCharAt(sb.lastIndexOf(" "));
        }
        return sb.toString();
    }
}
```

### 다른 사람의 풀이
```java
class Solution {
    public String solution(String s) {
        StringBuilder sb = new StringBuilder();
        String[] strings = s.toLowerCase().split("");
        boolean flag = true;
        for (String string : strings) {
            sb.append(flag ? string.toUpperCase() : string);
            flag = " ".equals(string) ? true : false;
        }
        return sb.toString();
    }
}
```
공백으로 문자열을 분리하지않고 모든 문자를 하나씩 탐색하면서 공백이 나온다음에는 대문자가 들어가게 했다.