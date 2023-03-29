# ***초급 2주차***

### **1051** 숫자 정사각형
##### 문제
> N×M크기의 직사각형이 있다. 각 칸에는 한 자리 숫자가 적혀 있다. 이 직사각형에서 꼭짓점에 쓰여 있는 수가 모두 같은 가장 큰 정사각형을 찾는 프로그램을 작성하시오. 이때, 정사각형은 행 또는 열에 평행해야 한다.

***
#### 코드
- ##### 석현
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
- ##### 경탁
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


#### 아이디어
- 입력받은 직사각형에 대해 가장 작은 정사각형일 경우부터 순서대로 탐색하여 꼭짓점의 숫자가 같은경우 정사각형의 크기를 출력.
- 가장 큰 정사각형일 경우부터 가장 작은 정사각형일 경우까지 전부 탐색한 후 꼭짓점의 숫자가 같은경우 가장 작은 정사각형의 크기를 출력.
- 꼭짓점 전부를 탐색하지 않고 직사각형의 시작점부터 대각선에 위치한 점들을 확인하여 같은 숫자일 경우 다른 꼭짓점들도 확인, 같다면 정사각형의 크기를 출력.
