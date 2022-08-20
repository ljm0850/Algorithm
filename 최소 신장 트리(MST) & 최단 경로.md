# 최소 신장 트리(MST) & 최단 경로

## 최소 신장 트리(MST)

- 그래프에서 최소 비용 문제
  - 모든 정점을 연결하는 간선들의 가중치 합이 최소가 되는 트리
  - 두 정점 사이의 최소 비용의 경로 찾기
- 신장 트리
  - n 개의 정점으로 이루어진 무방향 그래프에서 n개의 정점과 n-1개의 간선으로 이루어진 트리
  - 싸이클이 존재 x
- 최소 신장 트리(Minimum Spanning Tree)
  - 무방향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소인 신장 트리



### Prim 알고리즘

- 하나의 정점에서 연결된 간선들 중에 하나씩 선택하면서 MST를 만들어 가는 방식
  - 정점 한곳에서 시작
  - 선택한 정점과 인접한 정점중에 최소 비용의 간선이 존재하는 곳을 선택
  - 다시 선택된 정점들 중에서 위 과정 반복



### KRUSKAL 알고리즘

- 간선을 하나씩 선택해서 MST를 찾는 알고리즘
  - 최초, 모든 간선을 가중치에 따라 오름차순 정렬
  - 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가
  - 간선 선택시 사이클이 존재하게 될 경우, 포기하고 다음 간선 선택
  - 반복

```pytho
# 백준 1197
import sys
def solve(arr:list)->int:
    total = 0
    for node in arr: # 내림차순으로 정렬된것을 차례로 탐색
        if find_root(node[0]) != find_root(node[1]): # 연결된 적이 없는 노드간의 간선
            union(node[0],node[1])
            total += node[2]
    return total

def union(a:int,b:int)->None: # 선택된 노드를 연결
    A = find_root(a)
    B = find_root(b)
    if depth[A] > depth[B]:
        group[B] = A
    elif depth[A] < depth[B]:
        group[A] = B
    else:
        group[A] = B
        depth[B] += 1

def find_root(n:int)->int: # 노드의 root찾기(연결 상태 확인용)
    if group[n] == n:
        return n
    group[n] = find_root(group[n])
    return group[n]

V,E = map(int,sys.stdin.readline().split())
group = [num for num in range(V+1)]
depth = [1]*(V+1)
graph = [list(map(int,sys.stdin.readline().split())) for _ in range(E)]
graph.sort(key=lambda x:x[2])	# 오름차순 정렬
ans = solve(graph)
print(ans)
```





---

## 최단 경로

- 간선의 가중치가 있는 그래프에서 두 정점 사이의 경로들 중에 간선의 가중치 합이 최소인 경로
- 하나의 시작 정점에서 끝 정점까지의 최단 경로 
  - 다익스트라(dijkstra) 알고리즘
    - 음의 가중치를 허용하지 않음
  - 벨만-포드(Bellman-Ford) 알고리즘
    - 음의 가중치 허용

- 모든 정점들에 대한 최단 경로
  - 플로이드-워샬(Floyd-Warshall) 알고리즘



### Dijkstra(다익스트라) 알고리즘

- 시작 정점에서 거리가 최소인 정점들을 선택해 나가면서 최단 경로를 구하는 방식
- 탐욕 기법을 사용한 알고리즘으로 MST의 Prim과 유사



- 1에서 6로 가는 비용 최소화 문제라고 가정
  - 새로운 리스트 생성(index를 이용하여 1에서 각 지점까지 드는 비용 저장됨)
  - 선택된 노드를 저장할 list 생성 (list-a)
  - 1과 연결된 각 지점의 기본 비용을 리스트에 저장 , list-a에 1 추가
  - 그중 최소 비용 노드로 이동 (list-a에 해당 노드 추가)
  - 누적 형태로 리스트에 다음 노드(인접한 노드)까지 비용을 저장, 기존값이 있을 경우 둘중 낮은값으로 갱신
  - list-a가 가득 찰떄까지 반복