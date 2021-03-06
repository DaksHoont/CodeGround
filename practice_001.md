# 연습문제 \#1 숫자 골라내기
출처: https://www.codeground.org/practice

## 문제

초등학교교 학생인 정우와 석환이는 최근 학교에서 두 이진수의 XOR 연산에 대해 배웠다.
둘은 매우 영특한 학생이라 새로 배운 연산을 갖고 이리저리 장난치기 시작했다.
다만 석환이는 정우에게 일을 시키는 것을 좋아하는지라 다음과 같은 제안을 했다.

“내가 N 개의 10진수를 주면, 등장하는 숫자들 중 홀수번만 나타나는 숫자들을 모두 XOR 한 결과를 구해줘.”

예를 들어 '2, 5, 3, 3' 이 주어질 경우, '2'와'5'는 1번(홀수 번) 나타나고 '3' 은 2번 (짝수 번) 나타나므로 홀수 번 나타난 '2' 와 '5'를 XOR  한 결과를 구해야 하고, '2, 5, 3, 3, 2, 4, 5, 3' 이 주어질 경우 '2' 와 '5' 는 2번 나타나고, '3' 은 3번, '4' 는 1번 나타나므로 홀수 번 나타난 '3' 과 '4'를 XOR 한 결과를 구해야 한다.

정우는 제안을 수락했지만, 가면 갈수록 매번 XOR 연산을 수행하는 일에 지치고 있다. 정우를 도와서 주어 진 문제를 해결하는 프로그램을 작성하라.


#### 입력
입력 파일에는 여러 테스트 케이스가 포함될 수 있다.
파일의 첫째 줄에 케이스의 개수를 나타내는 자연수 T 가 주어지고, 이후 차례로 T 개의 테스트 케이스가 주어진다. ( 1≤T≤20 )
각각의 테스트 케이스 첫 번째 줄에는 석환이가 말한 숫자 N ( N  은 3,000,000 이하의 자연수)이 주어진다.
테스트 케이스의 둘째 줄에는 N개의 숫자들이 공백(빈칸)을 사이에 두고 주어진다.
각 숫자는 32bit 정수형 변수에 담을 수 있는 음이 아닌 정수이다.

#### 출력
각 테스트 케이스의 답을 순서대로 표준출력으로 출력하여야 하며, 각 테스트 케이스마다 첫 줄에는  “Case #T”를 출력하여야 한다. 이때 T는 케이스의 번호이다.
그 다음 줄에는 주어진 숫자들 중에서 '홀수' 번만 나타나는 숫자들을 모두 XOR 한 결과를 출력한다.

#### 입출력예
|   입력  |   출력  |
|--------|--------|
| 1 <br/> 4 <br/> 2 5 3 3 | Case #1 <br/> 7 |



## 풀이

자료구조나 알고리즘을 사용하지 않아도 풀 수 있는 문제라서, 프로그래밍 언어를 다룰 수 있으면 풀 수 있는 문제이다.

이런 문제의 핵심은 주어진 문제를 풀기 쉽고 효율적인 형태의 문제로 변환하는 것이다.

예를 들면 "3을 N번 더하시오" 라는 문제가 주어졌을 때, 단순히 3을 N번 더하는 프로그램을 만들어서 문제를 해결 할 수도 있지만, 3과 N을 곱하여 결과를 내는 프로그램이 훨씬 더 효율적이고, 코딩하기도 쉽다.

마찬가지로, 이번 문제도 제시된 문제 그대로 홀 수 번 나온 숫자들을 모아놓고, XOR 연산을 하는 방법도 있지만, 이렇게 하면 1) 숫자가 몇 번 나오는지 세는 함수, 2) 홀 수번 나온 숫자들을 XOR 하는 함수, 이렇게 두 부분을 프로그래밍 해야한다.

아마 이렇게 하면 프로그램이 복잡해 질 뿐만 아니라, 연산시간도 오래 걸려서 제한시간 내에 문제를 해결 할 수 없을 수도 있다.

XOR 연산의 특성을 이용하면, 주어진 문제를 훨씬 더 간단하게 바꿀 수 있다.

XOR 연산은 비트연산자이고, 1) 같은 비트(숫자)와 연산을 하면 0이 나오고, 2) 0과 XOR 연산을 하면 자기자신이 나온다는 특성이 있다.
따라서 주어진 모든 숫자를 XOR 연산하게 되면, 짝수번 나온 숫자는 0이 되어서 최종 결과에 영향을 미치지 않고, 결과적으로는 홀 수 번 나온 숫자끼리만 XOR 연산을 한 것과 같은 결과 낼 수 있다.

다시 한 번 정리하면 **홀 수 번 나온 숫자끼리 XOR 연산을 하라** 라는 문제는 **모든 숫자를 XOR 연산 하라** 라는 문제와 같은 결과를 가지는 것이다.

## 코드
입력된 모든 숫자를 XOR하는 프로그램을 구현한다.

### C
```c
// 코드그라운드로 알고리즘 공부하기
// https://github.com/DaksHoont/CodeGround

#include <stdio.h>

int Answer;

int main(void)
{
 int T, test_case;

 setbuf(stdout, NULL);

 scanf("%d", &T);
 for(test_case = 0; test_case < T; test_case++)
 {
     int i,N,x;
     Answer=0;

     scanf("%d", &N);
     for(i=0;i<N;i++)
     {
         scanf("%d",&x);
         Answer^=x;
     }

  printf("Case #%d\n", test_case+1);
        printf("%d\n", Answer);

 }

 return 0;
}
```
### C++
```c++
// 코드그라운드로 알고리즘 공부하기
// https://github.com/DaksHoont/CodeGround

#include <iostream>
using namespace std;

int res;

void solve()
{
	int N,i,a;
		
	cin>>N;

	res=0;
	for(i=0;i<N;i++)
	{
		cin>>a;
		res^=a;
	}
}

int main()
{
	int TC,test_case;

	cin>>TC;
	for(test_case=1;test_case<=TC;test_case++)
	{
		solve();

		cout<<"Case #"<<test_case<<endl
			<<res<<endl;
	}

	return 0;
}
```
    
### Python
```python
# 코드그라운드로 알고리즘 공부하기
# https://github.com/DaksHoont/CodeGround

import sys

inf = sys.stdin 

T = inf.readline();

for t in range(0, int(T)):
    
    Answer=0
    
    N = int(inf.readline())
    x_list = inf.readline().split()
    
    for x in x_list:
        Answer = Answer ^ int(x)
    
    print('Case #%d' %(int(t)+1))
    print(Answer)
    
inf.close()
```


