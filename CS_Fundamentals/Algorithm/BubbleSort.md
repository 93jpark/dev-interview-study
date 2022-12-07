버블 정렬(Bubble Sort)

이웃하는 숫자를 비교하여 작은 수를 앞쪽으로 띄워 정렬하는 알고리즘

​

버블 정렬 수행 과정

배열의 첫번째 원소와 두번째 원소를 비교해서 오름차순으로 자리를 바꾼다.

배열의 두번째 원소와 세번째 원소를 비교해서 오름차순으로 바꾸는 과정을 배열의 마지막까지 반복한다. 

위 과정을 전체적으로 1번 처리하는 것을 패스(pass)라고 하는데 1번의 패스가 끝나면 제일 큰 수가 맨 뒤에 고정된다. 

고정된 원소를 제외한 나머지 원소들로 배열 전체가 오름차순으로 정렬이 될 때까지 패스를 반복한다. 


​

수도코드(Pseudo Code)

입력: 크기가 n인 배열 A
출력: 정렬된 배열 A

for pass = 1 to n-1 
    for i = 1 to n-pass 
        if(A[i-1] > A[i]) // 위의 원소가 아래의 원소보다 크면
           A[i-1] ↔ A[i] // 자리바꿈
return A
n개의 원소에 대한 패스를 (n-1)번 수행하는 것은 원소가 최소 두 개가 있어야 패스가 가능하기 때문이다.

첫번째 for문은 배열을 정렬시키는 과정이고 두번째 for문은 최댓값을 찾는 과정이다. 

​

시간복잡도

 pass가 1이면 (n-1)번 비교하고 pass가 2면 (n-2)번 비교하고, ..., pass가 n-1이면 1번 비교한다. 따라서 총 비교횟수는 

$\left(n-1\right)+\left(n-2\right)+...+1=\sum _{k=1}^{n-1}k=\frac{n\left(n-1\right)}{2}$(n−1)+(n−2)+...+1=
n−1
∑
k=1k=
n(n−1)
2​​
이다.

2. 두번째 for-루프의 if-조건이 '참'일 때의  자리를 한 번 바꾸기 때문에 이때의 자리바꿈은 O(1)시간이 걸린다.

3. 버블 정렬의 시간복잡도는 

$\frac{n\left(n-1\right)}{2}\times \Omikron \left(1\right)=\Omikron \left(\frac{\combi{n}^2}{2}-\frac{n}{2}\right)=\Omikron \left(\combi{n}^2\right)$
n(n−1)
2​×Ο(1)=Ο(
n2
2​−
n
2​)=Ο(n2)​
이다.

​

버블 정렬 특징

가장 큰 수부터 맨 뒤에 하나씩 고정하는 한 번의 사이클 과정을 패스(pass)라고 한다.

시간복잡도가 느리지만 코드가 단순하다.

​

소스코드

C

#include <stdio.h> # define MAX 10 int* bubble_sort(int arr[], int n) { int i, j, temp; for (i=n-1; i>0; i--) { for (j=0; j<i; j++) { if (arr[j] > arr[j+1]) { temp = arr[j]; arr[j] = arr[j+1]; arr[j+1] = temp; } } } return arr; } int main() { int arr[MAX] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 }; int* arr_new = bubble_sort(arr, MAX); for (int i = 0; i < MAX; i++) { printf("%d\n", *(arr_new+i)); } return 0; }

C++

#include <iostream> using namespace std; #include <iomanip> using std::setw; void printBubbles(const int bubbles[], const int n); void lineup(int& large, int& small); int main() { const int n = 10; int bubbles[n] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 }; cout << "Data items in original order\n"; printBubbles(bubbles, n); for (int level = 0; level < n - 1; level++) { for (int i = 0; i < n - level - 1; i++) { if (bubbles[i] > bubbles[i + 1]) lineup(bubbles[i], bubbles[i + 1]); } } cout << "\nData items in ascending order\n"; printBubbles(bubbles, n); return 0; } void printBubbles(const int bubbles[], const int n) { for (int i = 0; i < n; i++) cout << setw(4) << bubbles[i]; cout << endl; } void lineup(int& large, int& small) { int save = large; large = small; small = save; }

C#

int[] data = new int[] { 3, 6, 2, 4, 1, 7, 9, 8, 5 }; int hold = 0; int[] BubbleSort = new int[] { }; for(int i = 0; i < data.Length - 1; i++) { for (int j = 0; j < data.Length - 1 - i; j++) { if (data[j] > data[j + 1]) { hold = data[j]; data[j] = data[j + 1]; data[j + 1] = hold; } } } for (int i = 0; i < data.Length; i++) { Console.WriteLine(data[i]); }

JAVA

void bubbleSort(int[] arr) { int temp = 0; for(int i = 0; i < arr.length - 1; i++) { for(int j= 1 ; j < arr.length-i; j++) { if(arr[j]<arr[j-1]) { temp = arr[j-1]; arr[j-1] = arr[j]; arr[j] = temp; } } } System.out.println(Arrays.toString(arr)); }

파이썬

def bubbleSort(x): length = len(x)-1 for i in range(length): for j in range(length-i): if x[j] > x[j+1]: x[j], x[j+1] = x[j+1], x[j] return x

​

reference

버블 정렬 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)

tech-refrigerator/bubble-sort-001.gif at master · GimunLee/tech-refrigerator (github.com)

양성봉. (2021). 알기 쉬운 알고리즘(개정판). 생능출판.