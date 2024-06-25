# K번째수
## 문제 설명
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.  

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면
1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.  

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한사항
* array의 길이는 1 이상 100 이하입니다.
* array의 각 원소는 1 이상 100 이하입니다.
* commands의 길이는 1 이상 50 이하입니다.
* commands의 각 원소는 길이가 3입니다.

## 풀이
### 나의 풀이
```java
import java.util.*;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        for(int i = 0; i < commands.length; i++) {
            int[] cutArr = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(cutArr);
            answer[i] = cutArr[commands[i][2] - 1];
        }
        
        return answer;
    }
}
```  
copyOfRange()를 사용해서 문제를 해결했다.

### API를 사용하지 않은 풀이
다른 사람의 풀이에 API를 사용해 푼 것에 대해서 비판하는 댓글을 볼 수 있다.  
개인적인 생각으로는 성능에 대한 체크를 하지 않으면 API를 사용하는 것이 좋다고 생각하지만, 성능에 대한 부분도 무시할 수 없기 때문에 API를 사용하지 않고 문제를 풀어봐야겠다.

```java
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        for(int i = 0; i < commands.length; i++) {
            int[] cutArr = new int[commands[i][1] - commands[i][0] + 1];
            
            for(int j = 0; j < cutArr.length; j++) {
                cutArr[j] = array[j+commands[i][0]-1];
            }
            
            sort(cutArr);
            
            answer[i] = cutArr[commands[i][2]-1];
        }
        
        return answer;
    }
    
    public void sort(int[] arr) {
        int temp = 0;
        
        for(int i = 0; i < arr.length - 1; i++) {
            for(int j = i+1; j < arr.length; j++) {
                if(arr[i] > arr[j]) {
                    temp = arr[j];
                    arr[j] = arr[i];
                    arr[i] = temp;
                }
            }
        }
    }
}
```
속도가 약 20배정도 빨라졌다.