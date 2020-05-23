# Exact Cover와 스도쿠

[스도쿠](https://en.wikipedia.org/wiki/Sudoku)는 널리 알려진 논리 퍼즐 중 하나로, 9 x 9 (또는 16 x 16) 표에 정해진 규칙대로 숫자를 채워 넣는 퍼즐이다. 

## Exact Cover 문제
Exact cover는 집합 X의 부분집합들이 있을 때, 이 중 몇 개를 골라 X의 모든 원소를 한 번만, 모두 가지는 부분집합의 조합을 찾는 문제이다. Exact cover는 스도쿠, N-Queen, 펜토미노 타일링과 같은 문제를 해결하는 데에도 사용된다. 간단한 예를 살펴보자.

전체집합 \\(X=\\left\\{1, 2, 3, 4\\right\\}\\) 에 대하여, 다음과 같은 부분집합들이 있다고 하자.

$$N=\\left\\{1, 2, 4\\right\\}, O=\\left\\{1, 3\\right\\}, P=\\left\\{2, 3\\right\\}, E=\\left\\{2, 4\\right\\}$$

이때 \\(O\\)와 \\(E\\)를 고르면, \\(O\\cup E=X\\)이고, \\(O\\cap E=\\varnothing\\)이므로 \\(O\\)와 \\(E\\)를 고르는 조합은 답이 된다. 반면, \\(N\\cup P=X\\)이지만, \\(N\\cap P\\neq\\varnothing\\)이므로 \\(N\\)과 \\(P\\)를 고르는 조합은 답이 될 수 없다. 이 문제를 컴퓨터가 풀게 하기 위해서는, 문제를 푸는 과정을 알고리즘으로 나타내어야 한다.

## 백트래킹
Exact cover는 [NP-완비](https://en.wikipedia.org/wiki/Np-complete) 문제이므로, 이 문제를 풀기 위해서는 모든 경우의 수를 시도해 보는 방법으로밖에 해결할 수 없다. 이러한 형태의 알고리즘 중에 대표적인 것으로 백트래킹 알고리즘이 있다. 백트래킹 알고리즘은 가능한 해를 반복적으로 만드는데, 만약 만들어낸 해가 적합하지 않다는 것이 판정되면 즉시 중단하고 다음 해로 넘어간다. 이렇게 설명하면 이해하기 힘드므로, 이 글에서 다루는 스도쿠로 예를 들어 보자.

스도쿠를 백트래킹 알고리즘으로 해결하려 할 때, 가장 단순하면서도 이해하기 쉬운 방법은 맨 윗줄의 빈칸부터 1부터 9까지 숫자를 넣어 보고, 만약 같은 행이나 열, 또는 박스 내에 같은 숫자가 있으면 이전 상태로 돌아가서 시도하는 것이다. 예를 들어 스도쿠를 푸는 중 다음과 같은 상황에 있다고 하자. (검은 숫자는 원래 있던 것이고, 파란 숫자는 알고리즘이 채운 숫자이다.)

TODO: 여기 그림 그리기

TODO: 설명 더 적기

하지만 이러한 방식으로 백트래킹을 할 경우, 얼마든지 이 알고리즘으로 푸는 것이 어려운 스도쿠를 만들 수 있다. 예를 들어, 만약 스도쿠의 맨 윗줄에서의 답이 987654321과 같은 순서라면 이 알고리즘의 경우 1부터 9까지, 1부터 8까지, ..., 1부터 2까지 한 줄의 답을 알기 위해 많은 연산을 해야 한다. 백트래킹 알고리즘에서는 효율적인 탐색 전략이 필요하다.

## Knuth's Algorithm X
Exact cover 문제를 푸는데 가장 많이 사용되는 알고리즘 중 하나로 Knuth's Algorithm X가 있다. 위에서 다룬 exact cover 문제를 알고리즘으로 해결해 보자.

우선 문제를 다음과 같이 행렬 형태로 나타내어야 한다. 행렬의 열은 각각의 집합의 열에 값이 포함되어 있는지를 나타낸다. 또한, 행렬의 행은 각각의 집합에 어떤 원소가 있는지를 나타낸다. 예를 들어, \\(1\\in N\\)이므로 행렬의 N행 1열 성분은 1이고, \\(2\\not\\in N\\)이므로 행렬의 N행 2열 성분은 0이다.

||1|2|3|4|
|--|--|--|--|--|
|N|1|0|1|1|
|O|1|0|1|0|
|P|0|1|1|0|
|E|0|1|0|1|

알고리즘은 재귀 함수의 형태로 구현되고, 행렬의 행과 열을 지웠다가 되돌리는 것을 반보

## 더 읽을거리
- [Dancing Links 원 논문](https://arxiv.org/pdf/cs/0011047.pdf): 이 글에서 설명하는 Knuth's Algorithm X, Dancing Links, DLX와 그 활용을 다룬 논문이다.
- [Wikipedia Exact Cover](https://en.wikipedia.org/wiki/Exact_cover): 
- [백준 3763번 스도쿠](https://www.acmicpc.net/problem/3763): 백준 온라인 저지에 있는 다른 스도쿠 문제와는 달리, 이 문제는 16 x 16 스도쿠를 풀어야 하기 때문에 여기에 설명된 방법을 사용해야 시간 제한 내에 해결할 수 있다.[^boj]

[^candy]: '캔디 크러쉬 사가'같은 게임을 플레이하는 느낌이 들 것이다.

[^skip]: 정 보기 싫으면 코드 설명으로 넘어가 코드를 읽자.

[^boj]: 문제를 풀고 싶다면, 여기 나온 코드를 그대로 복붙하지는 않도록 하자. [치팅으로 탐지](https://www.acmicpc.net/help/rule)되어 며칠동안 정지당할 수도 있다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ1MzcyMTA5MCwtMTEwNTQxNDAwNSwtMT
Y2NTQ2MTQwMiwxMDQ0NjMzNzc5LC0xMzYxODUyODEyLDE2MTQy
NTU1NDEsMTA4MjMxMTIzNiw1Mjg4MDc1NTAsMTY4MDMwODM3NS
wtODIyMDM4MTUwLC0yMTMxOTY3MDA4LC0xNDUwOTcwMzY0LC0y
MDk4MjI0MzQ3XX0=
-->