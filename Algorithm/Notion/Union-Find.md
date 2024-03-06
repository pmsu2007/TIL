# Union Find

Union Find는 **그래프 알고리즘**으로 서로소 집합(Disjoint-Set) 알고리즘으로 불린다.

Union Find는 **여러 개의 노드가 존재할 때 두 개의 노드를 선택해서, 현재 이 두 노드가 같은 그래프에 속하는지 판별**하는 알고리즘이다.

> ### Disjoint Set
>
> Disjoint Set은 서로소 집합 자료구조로, **서로 중복되지 않는 부분 집합**들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조
> <br/> <br/>

## Union Find의 연산

### make-set(x)

`make-set(x)` 는 **x를 유일한 원소로 하는 새로운 집합을 만드는 초기화 연산**이다.

### union(x, y)

`union(x, y)` 는 **x가 속한 집합과 y가 속한 집합을 합하는 연산**이다.

### find(x)

`find(x)`는 **x가 속한 집합의 루트 노드를 찾는 연산**이다.

