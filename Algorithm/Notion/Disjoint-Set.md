# Disjoint Set 

`Disjoint Set`은 서로소 집합으로 서로 공통된 원소를 가지고 있지 않은 두 개 이상의 집합을 말합니다.

Disjoint Set 자료구조를 사용하여 **서로 다른 원소들이 같은 집합에 속해 있는지 아닌지 판별**할 수 있습니다.

## Disjoint Set의 연산

1. `make-set()`

`make-set()` 연산은 **자신을 유일한 원소로 하는 집합을 만드는 초기화 연산**입니다.

이 연산에서 해당 노드의 부모 노드를 기록하는 Parent 배열을 생성합니다. 초기 값은 자기 자신을 부모 노드로 설정합니다.

```java
// make-set
public static void maekSet() {
    for (int i = 1; i <= N; i++) {
        parent[i] = i;
    }
}
```

2. `find()`

`find()` 연산은 **어떤 원소가 주어졌을 때 해당 원소가 속한 집합의 루트 노드를 반환하는 연산**입니다.

```java
public static int find(int x) {
    if (parent[x] == x) return x;

    return find(parent[x]);
}
```

3. `union()`

`union()` 연산은 두 개의 집합을 하나의 집합으로 합치는 연산입니다.

1. 각 원소에 `find()` 연산을 통해 해당 원소가 속한 집합의 루트 노드를 찾습니다.
2. 두 루트 노드 중 하나를 다른 루트 노드 밑에 배치하여 합칩니다. 일반적으로 루트 노드의 번호가 작은 쪽으로 연결합니다.

```java
public static void union(x, y) {
    int a = find(x);
    int b = find(b);

    if (a < b) parent[b] = a;
    else parent[a] = b; 
}
```

## Disjoint Set 연산 최적화

`union()`연산과 `find()` 연산의 성능은 **트리의 높이에 크게 의존**합니다. 따라서, 트리의 높이를 최소화해야 좋은 성능을 낼 수 있습니다.

트리의 높이를 줄일 수 있는 방법으로는 경로 압축(Path Compression)과 유니온 바이 랭크(Union By Rank)가 있습니다.

### 경로 압축 (Path Compression)

`경로 압축`은 `find()` 연산을 수행할 때 마다 트리의 구조를 평평하게 만드는 방법입니다.

`find()` 연산을 수행하면서 순회한 각 노드들을 직접 루트 노드를 가리키도록 하여 해당 집합에 속한 모든 노드들은 같은 루트 노드를 공유하게 됩니다.

```java
public static void find(x) {
    if (parent[x] == x) return x;

    parent[x] = find(parent[x]);
    
    return parent[x];
}
```

### 유니온 바이 랭크 (Union By Rank)

`유니온 바이 랭크`는 항상 작은 트리를 큰 트리 루트에 붙이는 방법입니다. 작은 트리는 상대적으로 높이가 낮거나 사이즈가 작은 트리를 말합니다. 

트리의 높이 or 사이즈를 저장하는 `rank` 배열을 활용합니다.

```java


// Union By Size
for (int i = 0; i < N; i++) {
    rank[i] = 1;
}
public static void union(int x, int y) {
    int a = find(x);
    int b = find(y);

    if (rank[a] < rank[b]) {
        parent[a] = b;
        rank[b] += rank[a];
    } else {
        parent[b] = a;
        rank[a] += rank[b];
    }
}
```