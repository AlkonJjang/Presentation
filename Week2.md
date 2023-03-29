# ***초급 2주차***

### **1051** 숫자 정사각형
#### 문제
> N×M크기의 직사각형이 있다. 각 칸에는 한 자리 숫자가 적혀 있다. 이 직사각형에서 꼭짓점에 쓰여 있는 수가 모두 같은 가장 큰 정사각형을 찾는 프로그램을 작성하시오. 이때, 정사각형은 행 또는 열에 평행해야 한다.

***
#### 나온 아이디어
1. 입력받은 직사각형에 대해 가장 작은 정사각형일 경우부터 순서대로 탐색하여 꼭짓점의 숫자가 같은경우 정사각형의 크기를 출력.
- cw, cl은 시작점에서 정사각형을 만들 수 있는 위치의 행, 열 인덱스를 나타냄. 시작점은 (0,0)에서부터 차례대로 하나씩. cw, cl 값이 커지며 정사각형 크기도 커짐 -> 작은 정사각형부터 모든 정사각형 탐색
- ```c++
  for (int i = 0; i < w; i++) {
      for (int j = 0; j < l; j++) {
          int cw = i + 1;
          int cl = j + 1;
          int last = -1;
          while (cw < w && cl < l) {
              if (arr[cw][cl] == arr[i][j] && arr[cw][j] == arr[i][j] && arr[i][cl] == arr[i][j]) {
                  last = cw;
              }
              cw++;
              cl++;
          }
          if (last != -1 && result < (last - i + 1) * (last - i + 1)) {
              result = (last - i + 1) * (last - i + 1);
          }

      }
  }
  ```

2. 입력받은 직사각형의 행, 열 중 작은 길이에 맞춰 정사각형 최대 크기를 설정, 가장 작은 정사각형 크기 부터 순차적으로 탐색. 1과 다른점 -> 한 점에서 정사각형 크기가 커지는것이 아닌 정사각형 크기가 n인 루프에서 모든 점 탐색 후 조건에 맞는 것이 없다면 n+1크기 정사각형 확인 루프 진행.
- 가장 바깥 for문이 정사각형 크기
- ```c++
  for (int i = 1; i < s + 1; i++)
    {
        for (int j = 0; j < n-i; j++)
        {
            for (int k = 0; k < m-i; k++)
            {
                if (arr[j][k] == arr[j + i][k] && arr[j][k] == arr[j][k + i] && arr[j][k] == arr[j + i][k + i])
                {
                    size = (i + 1) * (i + 1);
                }
            }
        }
    }
  ```



<br></br>
***
#### 코드
<details>
<summary>코드1</summary>

```c++
#include <iostream>
#include <string>
using namespace std;

int main() {
    int w, l;
    cin >> w >> l;
    if (w == 1 || l == 1) {
        cout << 1;
        return 0;
    }
    else {
        int result = 1;
        int arr[50][50] = { 0 };
        for (int i = 0; i < w; i++) {
            string str;
            cin >> str;
            for (int j = 0; j < l; j++) {
                arr[i][j] = str[j] - '0';
            }
        }

        for (int i = 0; i < w; i++) {
            for (int j = 0; j < l; j++) {
                int cw = i + 1;
                int cl = j + 1;
                int last = -1;
                while (cw < w && cl < l) {
                    if (arr[cw][cl] == arr[i][j] && arr[cw][j] == arr[i][j] && arr[i][cl] == arr[i][j]) {
                        last = cw;
                    }
                    cw++;
                    cl++;
                }
                if (last != -1 && result < (last - i + 1) * (last - i + 1)) {
                    result = (last - i + 1) * (last - i + 1);
                }

            }
        }
        cout << result;
    }
    return 0;
}
```
</details>

<details>
<summary>코드2</summary>

```c++
#include <iostream>
using namespace std;

int main()
{
    int n, m, b, s, size = 1;
    cin >> n >> m;
    char arr[50][50] ;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            cin >> arr[i][j];
        }
    }
    b = (n > m) ? n : m;
    s = (n < m) ? n : m;
    for (int i = 1; i < s + 1; i++)
    {
        for (int j = 0; j < n-i; j++)
        {
            for (int k = 0; k < m-i; k++)
            {
                if (arr[j][k] == arr[j + i][k] && arr[j][k] == arr[j][k + i] && arr[j][k] == arr[j + i][k + i])
                {
                    size = (i + 1) * (i + 1);
                }
            }
        }
    }
    printf("%d", size);
}
```
</details>

<br></br>
<br></br>

### **17359** 전구 길만 걷자
##### 문제
> 선린 친구들은 ✨인기스타 슈퍼인싸 예원쌤✨을 존경한다. 방학 동안 선생님을 뵐 수 없다니! 그래서 학생들은 방학식 날 💡전구 길만 걷자💡라는 엄청난 이벤트를 준비했다.<br><br>
💡💡💡💡👨‍🏫💡💡💡💡<br><br>
아무도 몰랐지만, 사실 선린의 과학실에는 전구가 일렬로 이어진 전구 묶음이 N개 있다. 학생들은 이 묶음을 일렬로 이어 전구 길을 만들기로 했다. 하지만 묶음에는 불이 들어오지 않는 전구가 섞여 있었는데, 전구들을 일렬로 이어 놓으니 켜진 전구와 꺼진 전구가 번갈아 나타나서 전구 길이 예쁘지 않았다.<br><br>
그래서 학생들은 전구 길이 최대한 예쁘도록 묶음을 배열하려고 한다. 전구 길은 전구 상태가 바뀌는 횟수가 최소일 때 가장 예쁘다고 한다. 이는 켜진 전구를 1, 꺼진 전구를 0이라 했을 때, 전구 길에 01 또는 10이 최소로 나타나야 한다는 의미이다.<br><br>
예를 들어, (1011) 묶음과 (1000) 묶음을 이어 붙여야 한다고 하자. 이때는 (10111000) 순서로 잇는 것이 (10001011) 순서로 잇는 것보다 예쁘다. 전자는 전구의 상태가 3번 바뀌고, 후자는 전구의 상태가 4번 바뀌기 때문이다.<br><br>
그런데 갑자기 세한이가 코드를 작성해서 이를 계산하자고 한다.
세한이와 함께 전구 길을 예쁘게 꾸며보자!

***
#### 코드
