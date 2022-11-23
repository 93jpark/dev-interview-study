선택 정렬(Select Sort)

현재 위치에 들어갈 값을 선택해서 오름차순으로 정렬하는 알고리즘

​

배열 전체에서 최솟값을 '선택'하여 배열의 0번 원소와 자리를 바꾼다.

배열의 0번을 고정시키고 나머지 배열에서 위 과정을 반복한다. 


SelectionSort

 수도코드(Pseudo Code : 가짜의 코드)

입력: 크기가 n인 배열 A
출력: 정렬된 배열 A

for i = 0 to n-2 {

    min = i

    for j = i + 1 to n-1 {

        if (A[j] < A[min])

           min = j

      }

    A[i] <-> A[min]

  }

return 배열 A

﻿
크기가 n인 배열에서 index 0부터 시작하기 때문에 배열 A는 0부터 n-1까지의 index가 있다. 

첫번째 for문이 n-2까지인 것은 j가 i+1이기 때문에 범위를 벗어나지 않게 n-2로 설정했다. 

첫번째 for문은 pivot(기준점)을 두기 위한 반복문이고, 두번째 for문은 최솟값 찾기 위한 반복문이다.

 

시간복잡도

첫번째 for문은 0부터 (n-2)까지 (n-1)번 수행되고 두번째 for문은 첫번째 for문이 0일 때 n-1번, 1일 때 n-2번......(n-2)일 때 1번 수행되므로 총 횟수는 

$(n-1)+(n-2)+(n-3)+...+2+1=\sum _{k=1}^{n-1}k\ =\ \frac{n\left(n-1\right)}{2}$(n−1)+(n−2)+(n−3)+...+2+1=
n−1
∑
k=1k = 
n(n−1)
2​​
이다.

2. 두번째 for문 내부의 if-조건이 '참'일 때 자리바꿈의 연산횟수가 한번이기 때문에 O(1)(오원)시간이 걸린다.

3. 선택 정렬의 시간복잡도는 

$\frac{n\left(n-1\right)}{2}\times \Omikron \left(1\right)=\Omikron \left(\frac{\combi{n}^2}{2}-\frac{n}{2}\right)=\Omikron \left(\combi{n}^2\right)$
n(n−1)
2​×Ο(1)=Ο(
n2
2​−
n
2​)=Ο(n2)​
이다.

​

선택 정렬 특징

원소 간의 비교 횟수는 많지만 자리바꿈 횟수가 최소이다.

제자리 정렬(in-place sorting)을 하는 형태로 다른 메모리 공간을 필요로 하지 않아 공간 복잡도는 O(1) 이다.

입력에 민감하지 않고 항상 일정한 시간복잡도를 나타낸다.

​

소스코드

Java

void selectionSort(int[] list) { int indexMin, temp; for (int i = 0; i < list.length - 1; i++) { indexMin = i; for (int j = i + 1; j < list.length; j++) { if (list[j] < list[indexMin]) { indexMin = j; } } temp = list[indexMin]; list[indexMin] = list[i]; list[i] = temp; } }

temp - 순서 바꾸기

C

void selectionSort(int *list, const int n) { int i, j, indexMin, temp; for (i = 0; i < n - 1; i++) { indexMin = i; for (j = i + 1; j < n; j++) { if (list[j] < list[indexMin]) { indexMin = j; } } temp = list[indexMin]; list[indexMin] = list[i]; list[i] = temp; } }

Objective Caml(OCaml)

let rec ssort = function | [] -> [] | h::t -> (ssort (etcList (findMax h t) (h::t))) @ [(findMax h t)] and findMax a = function | [] -> a | h::t -> if a>h then (findMax a t) else (findMax h t) and etcList a = function | [] -> [] | h::t -> if h=a then t else h :: (etcList a t);;

파이썬

def selectionSort(x): length = len(x) for i in range(length-1): indexMin = i for j in range(i+1, length): if x[indexMin] > x[j]: indexMin = j x[i], x[indexMin] = x[indexMin], x[i] return x

reference

선택 정렬 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)

선택 정렬(Selection Sort) | 👨🏻‍💻 Tech Interview (gyoogle.dev)

[알고리즘] 선택정렬(Selection Sort)이란? | c언어 선택정렬 구현 (tistory.com)

양성봉. (2021). 알기 쉬운 알고리즘(개정판). 생능출판.