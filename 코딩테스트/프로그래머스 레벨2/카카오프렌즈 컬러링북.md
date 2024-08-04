# 카카오프렌즈 컬러링북
## 문제 설명
출판사의 편집자인 어피치는 네오에게 컬러링북에 들어갈 원화를 그려달라고 부탁하여 여러 장의 그림을 받았다.  
여러 장의 그림을 난이도 순으로 컬러링북에 넣고 싶었던 어피치는 영역이 많으면 색칠하기가 까다로워 어려워진다는 사실을 발견하고 그림의 난이도를 영역의 수로 정의하였다.  
(영역이란 상하좌우로 연결된 같은 색상의 공간을 의미한다.)

그림에 몇 개의 영역이 있는지와 가장 큰 영역의 넓이는 얼마인지 계산하는 프로그램을 작성해보자.

## 제한 조건
* 1 <= m, n <= 100
* picture의 원소는 0 이상 2^31 - 1 이하의 임의의 값이다.
* picture의 원소 중 값이 0인 경우는 색칠하지 않는 영역을 뜻한다.

## 풀이
### 나의 풀이
```java
class Solution {
    public int[] solution(int m, int n, int[][] picture) {
        boolean[][] pictureFlag = new boolean[m][n];
        int numberOfArea = 0;
        int maxSizeOfOneArea = 0;
        
        for (int i = 0; i < picture.length; i++) {
            for (int j = 0; j < picture[i].length; j++) {
                if(picture[i][j] == 0 || pictureFlag[i][j]) {
                    pictureFlag[i][j] = true;
                    continue;
                }

                numberOfArea++;
                int areaSize = calAreaSize(0, i, j, picture[i][j], picture, pictureFlag);
                if(areaSize > maxSizeOfOneArea) maxSizeOfOneArea = areaSize;
            }
        }
        
        int[] answer = {numberOfArea, maxSizeOfOneArea};
        return answer;
    }
    
    int calAreaSize(int areaSize, int i, int j, int targetNum, int[][] picture, boolean[][] pictureFlag) {
        if(i < 0 || i >= picture.length || j < 0 || j >= picture[i].length || pictureFlag[i][j]) return areaSize;
        if(picture[i][j] == targetNum) {
            areaSize += 1;
            pictureFlag[i][j] = true;
        } else return areaSize;

        areaSize = calAreaSize(areaSize, i+1, j, targetNum, picture, pictureFlag);
        areaSize = calAreaSize(areaSize, i-1, j, targetNum, picture, pictureFlag);
        areaSize = calAreaSize(areaSize, i, j+1, targetNum, picture, pictureFlag);
        areaSize = calAreaSize(areaSize, i, j-1, targetNum, picture, pictureFlag);

        return areaSize;
    }
}
```  
boolean 배열을 만들어서 0이나 한 번 확인한 자리라면 true로 만들어서 체크한 영역은 다시 체크 안하도록 만든 후  
false인 요소는 상,하,좌,우 모두 확인해서 targetNum과 똑같은지 확인한다.
