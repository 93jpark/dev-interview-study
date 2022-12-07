삽입 정렬(Insertion Sort)

정렬되지 않은 부분의 배열의 원소를 순서대로, 정렬된 부분의 배열과 각각 비교하여 오름차순으로 적절한 위치에 삽입하여 정렬을 완성하는 알고리즘


​

실행 과정

배열을 정렬된 부분과 정렬되지 않은 부분으로 나눈다.

정렬되지 않은 부분의 첫번째 원소부터 왼쪽의 정렬된 원소와 비교하면서 한칸씩 이동한다. 

정렬된 부분의 원소 사이에 오름차순으로 적절한 위치에 삽입한다.

정렬되지 않은 원소를 차례대로 위 과정을 반복한다. 

​

수도 코드(Pseudo Code)

입력: 크기가 n인 배열 A
출력: 정렬된 배열 A

for i = 1 to n-1 {
    CurrentElement = A[i] // 현재 원소는 정렬이 안 된 부분의 가장 왼쪽 원소
    j <- i-1 // 정렬된 부분의 가장 오른쪽 원소
    while (j >= 0) and (A[j] > CurrentElement) {
          A[j+1] = A[j] // CurrentElement와 자리 변경
          j <- j-1 // while-루프를 반복적으로 수행 
         }
    A[j+1] <- CurrentElement //그 자리에 삽입
  }
return A
index 0은 정렬된 부분이기 때문에 에 index 1부터 정렬을 시작한다.

크기가 n인 배열에서 위와 같은 이유로 i가 1부터 n-1까지 이다.

while의 첫번째 조건은 배열의 범위가 0부터이기 때문에 나오는 기본 조건이다.

while문에서 j는 비교 대상이 되는 원소이고 j와 CurrentElement를 비교한다.

원소를 정렬하기 위하여 CurrentElement보다 큰 원소들의 자리를 이동시킨다.

​

시간복잡도

1.i는 1부터 (n-1)이기 때문에 for-루프가 (n-1)번 수행된다.

2. while-루프는 i가 1일 때 1번, 2일때 2번...(n-1)일 때 (n-1)번 수행되므로,

$1+2+3+...+\left(n-2\right)+\left(n-1\right)=\sum _{k=1}^{n-1}k=\frac{n\left(n-1\right)}{2}$1+2+3+...+(n−2)+(n−1)=
n−1
∑
k=1k=
n(n−1)
2​​
이다.

3. while-루프 조건이 성립할 때 자리 바꿈 연산 횟수가 1번이기 때문에 

while-루프의 수행시간은 O(1)이다.

4. 삽입 정렬이 시간복잡도는 

$\frac{n\left(n-1\right)}{2}\times \Omikron \left(1\right)=\Omikron \left(n^2\right)$
n(n−1)
2​×Ο(1)=Ο(n2)​
이다.

​

삽입정렬 특징

배열의 첫번째 부분만 정렬된 상태에서 시작한다. 

입력의 크기가 작을 때 매우 좋은 성능을 보인다.

퀵 정렬, 합병 정렬에서 입력 크기가 작아지면 순환 호출을 중단하고 삽입 정렬을 사용한다.

Tim sort에서는 입력 크기가 64이하이면 삽입 정렬을 호출한다.

최선의 경우에는 입력이 이미 정렬되어 자리이동이 없다면(while-루프가 실행되지 않는다면) 시간복잡도는

$\left(n-1\right)\times \Omikron \left(1\right)=\Omikron \left(n\right)$(n−1)×Ο(1)=Ο(n)​
이다.

​

소스코드

JAVA

void insertionSort(int[] arr) { for(int index = 1 ; index < arr.length ; index++){ int temp = arr[index]; int aux = index - 1; while( (aux >= 0) && ( arr[aux] > temp ) ) { arr[aux + 1] = arr[aux]; aux--; } arr[aux + 1] = temp; } }

C

void insertion_sort ( int *data, int n ) { int i, j, remember; for ( i = 1; i < n; i++ ) { remember = data[(j=i)]; while ( --j >= 0 && remember < data[j] ){ data[j+1] = data[j]; } data[j+1] = remember; } }

아래는 정렬되는 자료가 단순 데이터일 경우에 memcpy()를 이용하여 자료를 밀어내는 예제이다. memcpy()는 자료를 당겨야하므로 비교를 역순으로 수행한다. 위의 코드보다 25~30% 가량 빠르게 처리된다.

void insertion_sort ( int *data, int n ) { int i, j, remember; i = n-1; while ( i-- > 0 ) { remember = data[(j=i)]; while ( ++j < n && remember > data[j] ); if ( --j == i ) continue; memcpy ( data+i, data+i+1, sizeof(*data) * (j-i) ); data[j] = remember; } }

C++

#include <iterator> template<typename biIter> void insertion_sort(biIter begin, biIter end) { biIter bond = begin; for (++bond; bond!=end; ++bond) { typename std::iterator_traits<biIter>::value_type key = *bond; biIter ins = bond; biIter pre = ins; } }

파이썬​

def insert_sort(x): for i in range(1, len(x)): j = i - 1 key = x[i] while x[j] > key and j >= 0: x[j+1] = x[j] j = j - 1 x[j+1] = key return x

​

reference

삽입 정렬 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)

양성봉. (2021). 알기 쉬운 알고리즘(개정판). 생능출판.