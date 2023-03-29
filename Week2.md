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
- 가장 바깥 for문이 정사각형 크기. s는 행, 열 중 작은쪽의 크기
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
#### 문제
> 선린 친구들은 ✨인기스타 슈퍼인싸 예원쌤✨을 존경한다. 방학 동안 선생님을 뵐 수 없다니! 그래서 학생들은 방학식 날 💡전구 길만 걷자💡라는 엄청난 이벤트를 준비했다.<br><br>
💡💡💡💡👨‍🏫💡💡💡💡<br><br>
아무도 몰랐지만, 사실 선린의 과학실에는 전구가 일렬로 이어진 전구 묶음이 N개 있다. 학생들은 이 묶음을 일렬로 이어 전구 길을 만들기로 했다. 하지만 묶음에는 불이 들어오지 않는 전구가 섞여 있었는데, 전구들을 일렬로 이어 놓으니 켜진 전구와 꺼진 전구가 번갈아 나타나서 전구 길이 예쁘지 않았다.<br><br>
그래서 학생들은 전구 길이 최대한 예쁘도록 묶음을 배열하려고 한다. 전구 길은 전구 상태가 바뀌는 횟수가 최소일 때 가장 예쁘다고 한다. 이는 켜진 전구를 1, 꺼진 전구를 0이라 했을 때, 전구 길에 01 또는 10이 최소로 나타나야 한다는 의미이다.<br><br>
예를 들어, (1011) 묶음과 (1000) 묶음을 이어 붙여야 한다고 하자. 이때는 (10111000) 순서로 잇는 것이 (10001011) 순서로 잇는 것보다 예쁘다. 전자는 전구의 상태가 3번 바뀌고, 후자는 전구의 상태가 4번 바뀌기 때문이다.<br><br>
그런데 갑자기 세한이가 코드를 작성해서 이를 계산하자고 한다.
세한이와 함께 전구 길을 예쁘게 꾸며보자!

***
#### 나온 아이디어 
1. 먼저 묶음 내부의 점수는 전부 계산 <br>
1_0 형태와 0_1 형태의 묶음이 없고 0_0, 1_1 형태의 묶음이 둘다 있다 -> +1<br>
1_0, 0_1 묶음이 있다 -> 둘의 갯수 차이만큼 +1, <br>
1_0 형태와 0_1 형태의 묶음이 없고 0_0, 1_1 형태의 묶음중 한종류만 존재 -> 점수 변화 없음.
- ```c++
  if (lto == 0 && otl == 0) 
      if(ltl != 0 && oto != 0) ans++;
	  else ans += abs(lto - otl);
  ```

2. 0_0과 1_1형태는 최대 1개로 생각. 0_1이나 1_0형태가 하나라도 있다면 0_0과 1_1 형태는 0개로 간주. 내부 점수 계산결과에 0_0 + abs(0_1 - 1_0) + 1_1의 결과를 더함
-   ```c++
    // 0_1, 1_0, 1_1, 0_0 추가 조건문
    if (str[0] == '0' && str[(int)str.length() - 1] == '0' && z_z == 0) { // 0_0은 최대 1개
        z_z++;
    }
    else if (str[0] == '0' && str[(int)str.length() - 1] == '1') {
        z_o++;
    }
    else if (str[0] == '1' && str[(int)str.length() - 1] == '0') {
        o_z++;
    }
    else if (str[0] == '1' && str[(int)str.length() - 1] == '1' && o_o==0) { // 1_1은 최대 1개
        o_o++;
    }
    ```
- ```c++
  if(z_o>0||o_z>0){
        o_o = 0;
        z_z = 0;
    }
  
    int add = o_o + abs(z_o - o_z) + z_z;
    if (add > 1) {
        result += add - 1;
    }
  ```

***
#### 코드
<details>
<summary>코드1</summary>

```c++
#include <iostream>
#include <cmath>

using namespace std;

int main()
{
	int n, ans = 0 ;
	int oto=0;
	int lto=0;
	int otl=0;
	int ltl=0;
	cin >> n;
	char arr[10][100] = {};
	char hnt[10][3] = {};
	for (int i = 0; i < n; i++)
	{
		cin >> arr[i];
	}
	for (int i = 0; i < n; i++)
	{
		hnt[i][0] = arr[i][0];
		for (int j = 0; j < 100; j++)
		{
			if (arr[i][j] != arr[i][j + 1])
				if (arr[i][j + 1] == '\n' || arr[i][j + 1] == '\0')
				{
					hnt[i][1] = arr[i][j];
					break;
				}
				else	ans++;
		}
	}
	for (int i = 0; i < n; i++)
	{
		if (hnt[i][0] == '0'&& hnt[i][1] == '0') oto++;
		else if (hnt[i][0] == '1' && hnt[i][1] == '0') lto++;
		else if (hnt[i][0] == '0' && hnt[i][1] == '1') otl++;
		else if (hnt[i][0] == '1' && hnt[i][1] == '1') ltl++;
	}
	if (lto == 0 && otl == 0) 
		if(ltl != 0 && oto != 0) ans++;
	else ans += abs(lto - otl);
	cout << ans;
}
```
</details>
<details>
<summary>코드2</summary>

```c++
#include <iostream>
#include <string>
using namespace std;

int main() {
    int num;
    cin >> num;
    int result = 0;
    int o_o = 0;
    int z_z = 0;
    int z_o = 0;
    int o_z = 0;

    for (int i = 0; i < num; i++) {
        string str;
        cin >> str;
        for (int j = 0; j < (int)str.length() - 1; j++) {
            if (str[j] != str[j + 1]){
                result++;
            }
        }
        if (str[0] == '0' && str[(int)str.length() - 1] == '0' && z_z == 0) {
            z_z++;
        }
        else if (str[0] == '0' && str[(int)str.length() - 1] == '1') {
            z_o++;
        }
        else if (str[0] == '1' && str[(int)str.length() - 1] == '0') {
            o_z++;
        }
        else if (str[0] == '1' && str[(int)str.length() - 1] == '1' && o_o==0) {
            o_o++;
        }
    }
    if(z_o>0||o_z>0){
        o_o = 0;
        z_z = 0;
    }
  
    int add = o_o + abs(z_o - o_z) + z_z;
    if (add > 1) {
        result += add - 1;
    }
    
    cout << result << "\n";
    return 0;
}
```
</details>

<br></br>
<br></br>

### **12348** 분해합 2
#### 문제
> 어떤 자연수 N이 있을 때, 그 자연수 N의 분해합은 N과 N을 이루는 각 자리수의 합을 의미한다. 어떤 자연수 M의 분해합이 N인 경우, M을 N의 생성자라 한다. 예를 들어, 245의 분해합은 256(=245+2+4+5)이 된다. 따라서 245는 256의 생성자가 된다. 물론, 어떤 자연수의 경우에는 생성자가 없을 수도 있다. 반대로, 생성자가 여러 개인 자연수도 있을 수 있다.<br><br>
자연수 N이 주어졌을 때, N의 가장 작은 생성자를 구해내는 프로그램을 작성하시오.
***
#### 나온 아이디어
1. 입력값의 최댓값은 10의 18제곱. 따라서 생성자의 각 자릿수 합의 최댓값은 9*17 = 153이므로 153에서 하나씩 줄여가며 최소 생성자를 구함
- dig는 각 자리 수를 저장. 각 자리수 합이 가장 클 때가 생성자가 최소 -> 153에서 하나씩 줄여나가다 조건에 맞다면 t=1해주고 루프 종료
-   ```c++
    for (int i = 153; i > 0; i--)
	{
		sum = 0;
		m = n - i;
		for (int j = 0; j < 19; j++)
		{
			dig[j] = m - (m / 10) * 10;
			m = m / 10;
		}
		for (int j = 0; j < 19; j++) sum += dig[j];
		if (sum == i)
		{
			t = 1;
			m = n - i;
			break;
		}
	}
    ```

2. log함수를 통해 자릿수를 구하고 그 자릿수에 9를 곱한것 + 10^자릿수-1을 해 그 자릿수에서의 최소 생성자를 산출 -> i를 1씩 늘려가며 조건에 맞는 경우 루프 종료
-   ```c++
    int size = floor(log10(num) + 1);
    int min = (size - 1) * 9 + num / pow(10, size - 1) - 1;

    for (long long i = num - (min); i < num; i++) {
        long long sum = 0;
        long long cur = i;
        while (cur > 0) {
            sum += cur % 10;
            cur = cur / 10;
        }
        if (sum + i == num) {
            printf("%lld", i);
            return 0;
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

int main()
{
	long long n = 0, m = 0;
	int sum = 0, t = 0;
	char dig[19] = {};
	cin >> n;
	for (int i = 153; i > 0; i--)
	{
		sum = 0;
		m = n - i;
		for (int j = 0; j < 19; j++)
		{
			dig[j] = m - (m / 10) * 10;
			m = m / 10;
		}
		for (int j = 0; j < 19; j++) sum += dig[j];
		if (sum == i)
		{
			t = 1;
			m = n - i;
			break;
		}
	}
	if (t == 1) cout << m << '\n';
	else cout << '0' << '\n';
}
```
</details>

<details>
<summary>코드2</summary>

```c++
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

int main() {
    long long num;
    cin >> num;
    if (num < 10) {
        if (num % 2 == 0) {
            printf("%lld", num / 2);
        }
        else {
            printf("%d", 0);
        }
        return 0;
    }
    int size = floor(log10(num) + 1);
    int min = (size - 1) * 9 + num / pow(10, size - 1) - 1;

    for (long long i = num - (min); i < num; i++) {
        long long sum = 0;
        long long cur = i;
        while (cur > 0) {
            sum += cur % 10;
            cur = cur / 10;
        }
        if (sum + i == num) {
            printf("%lld", i);
            return 0;
        }
    }
    printf("%d", 0);
    return 0;
}
```
</details>

<br></br>
<br></br>
