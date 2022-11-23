
# 알고리즘


## :memo: Table of Contents

- [트리](#트리tree)
    - [개념](#트리tree의-개념)
    - [용어](#트리tree와-관련된-용어)
    - [특징](#트리tree의-특징)
    - [트리의 종류](#트리tree의-종류)
        - [트리 vs 이진트리](#트리-vs-이진-트리)
    - [트리 순회](#이진트리의-순회-방법)
        - [전위 순회](#전위-순회)
        - [중위 순회](#중위-순회)
        - [후위 순회](#후위-순회)
    - [Complete Binary Tree](#complete-binary-tree)

<br>

---

<br>

## 트리(Tree)


### 트리(Tree)의 개념
- 무방향이면서 사이클이 없는 연결 그래프(Undirected Acyclic Connected Graph)이다. <br>
- 연결 그래프이면서 임의의 간선을 제거하면 연결 그래프가 아니게 되는 그래프<br>
- 임의의 두 점을 연결하는 simple path(정점이 중복해서 나오지 않는 경로)가 유일한 그래프<br>
- V개의 정점을 가지고 V-1개의 간선을 가지는 연결 그래프<br>
- 사이클이 없는 연결 그래프이면서 임의의 간선을 추가하면 사이클이 생기는 그래프<br>
    - **V개의 정점을 가지고 V-1개의 간선을 가지는 Acyclic(=사이클이 없는) 그래프**

* 주의: 정점이 1개이면서 간선이 없는 그래프도 트리이다.

<br><br>

### 트리(Tree)와 관련된 용어
![image](https://user-images.githubusercontent.com/43839951/200528702-f7e71b97-bc97-42b2-9961-93461f8e2913.png)
- 루트 노드(root node): 부모가 없는 노드, 트리 구조에서 최상위에 존재하는 노드.<br>
- 단말 노드(leaf node): 자식이 없는 노드, ‘말단 노드’ 또는 ‘잎 노드’라고도 부른다.<br>
- 내부(internal) 노드: 단말 노드가 아닌 노드<br>
- 간선(edge): 노드를 연결하는 선 (link, branch 라고도 부름)<br>
- 형제(sibling): 같은 부모를 가지는 노드<br>
- 노드의 크기(size): 자신을 포함한 모든 자손 노드의 개수<br>
- 노드의 깊이(depth): 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수<br>
- 노드의 레벨(level): 트리의 특정 깊이를 가지는 노드의 집합<br>
- 노드의 차수(degree): 하위 트리 개수 / 간선 수 (degree) = 각 노드가 지닌 가지의 수<br>
- 트리의 차수(degree of tree): 트리의 최대 차수<br>
- 트리의 높이(height): 루트 노드에서 가장 깊숙히 있는 노드의 깊이<br>
 
<br><br>

### 트리(Tree)의 특징
- **그래프**의 한 종류이다
- **계층 모델**이다
- **loop, circuit**이 없다(사이클이 없다)
- 노드가 N개인 트리는 **N-1개의 간선**을 가진다
- 루트에서 특정 노드로 가는 **경로는 유일**하다(두 개의 정점 사이에 반드시 1개의 경로만을 가진다)

<br><br>

### 트리(Tree)의 종류

#### 트리 VS 이진 트리
트리는 `서브 트리`로 구성된다. `서브 트리`는 더 작은 서브 트리들로 구성된다.<br>
위 개념을 적용하여 정의한 이진 트리의 조건은 다음과 같다.
- 루트 노드를 중심으로 두 개의 서브 트리로 나뉘어진다.
- 나뉘어진 두 서브 트리로 모두 이진 트리이어야 한다.

여기서 주의 할 점은 공집합 또한 이진트리의 노드로 취급한다는 점이다.<br><br>

<img src="https://user-images.githubusercontent.com/43839951/200601409-e376d17c-f353-46f8-b9f3-7b677fe9da62.png" width="350" height="150"/>
<br><br>

### 이진트리의 순회 방법
이진트리는 순회의 방식에 따라 `전위순회`, `중위순회`, `후위순회`로 나눌 수 있다.<br>
실제 코드를 통하여 순회 방식을 비교해 본다.<br><br>
#### 전위 순회
```python
# 방문 순서 : 루트 -> 왼 -> 오
def preorder(v):
    print(chr(v+65),end = '')
    if left[v] != -1:
        preorder(left[v])
    if right[v] != -1:
        preorder(right[v])
```
전위 순회란 트리의 `루트 노드`를 가장 먼저 순회하는 방식이다. 
코드에서는 print문을 통하여 방문 노트 순서를 보여준다.<br><br>

#### 중위 순회
```python
# 방문 순서 : 왼 -> 루트 -> 오
def preorder(v):
    if left[v] != -1:
        preorder(left[v])
    print(chr(v+65),end = '')
    if right[v] != -1:
        preorder(right[v])
```
중위 순회는 `루트 노드`를 중간에 순회한다.<br><br>

#### 후위 순회
```python
# 방문 순서 : 왼 -> 오 -> 루트
def preorder(v):
    if left[v] != -1:
        preorder(left[v])
    if right[v] != -1:
        preorder(right[v])
    print(chr(v+65),end = '')
```

위의 세가지 예시에서 알 수 있 듯 결국 재귀 함수를 호출하여 트리의 `서브 트리`를
순회하는 과정에서 루트 노드를 언제 방문했는지의 차이만 있을 뿐임을 알 수 있다.<br><br>

<br><br>
## Full Binary Tree
- 모든 레벨이 꽉 차 있는 트리
- 노드를 더 추가하려면 **레벨을 늘려야 한다**.<br><br>
<img src="https://user-images.githubusercontent.com/43839951/200601711-960bee3e-a107-4acf-906c-3cebf16195de.png" width="200" height="200"/>
<br><br>

### Complete Binary Tree
- `Full Binary Tree`에서 레벨을 하나 더 늘려서 H,I를 추가한다고 가정하자
- 모든 레벨이 꽉 찬 상태는 아니지만, **빈틈없이 노드가 채워진** 이진 트리를 의미한다.

> 빈틈없이 노드가 채워진: 노드가 위->아래, 왼쪽 -> 오른쪽의 순서대로 채워진 상태


<img src="https://user-images.githubusercontent.com/43839951/200601931-31269a28-9517-46bf-a355-83cb58ac3264.png" width="200" height="200"/>


<br><br>

>Reference
[[자료구조] 트리(Tree)란](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)


