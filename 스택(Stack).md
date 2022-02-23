# 스택(Stack)

## 스택

- 자료를 쌓아 올린 형태의 자료구조
- 선형 구조를 가짐
  - 선형구조 : 자료 간의 관계가 1:1
  - 비선형구조: 자료간의 관계가 1:N
- 마지막에 삽입한 자료를 가장 먼저 꺼낸다(후입선출Last-In-First_Out)
- top : 마지막 삽입된 원소의 위치



## 연산

```python
class stack:
    def __init__(self):
        self.items = []
        self.top = -1

    def push(self,item):
        self.top +=1
        self.items.append(item)

    def pop(self,item):
        value = self.items[self.top]
        self.items[self.top] = None
        self.top -= 1
        return value
    
    def isEmpty(self):
        if self.top == -1:
            return True
        else:
            return False
    
    def peek(self):
        return self.items[self.top]
```

- push(삽입)
  - 자료를 저장, append를 통해 리스트의 마지막에 데이터 삽입
- pop(삭제)
  - 삽입한 자료의 역순으로 자료를 꺼냄
- isEmpty
  - 스택이 공백인지 확인
- peek
  - 스택의 top에 있는 item을 반환



## 재귀호출

```python
#피보나치 수열 재귀
def fibo(n):
    if n < 2 :
        return n
    else:
        return fibo(n-1) + fibo(n-2)
```

- 자기 자신을 호출하여 순환

- 간단하게 작성이 가능한 장점이 있음
- 중복된 함수호출로 인한 시간지연이 문제



## Memoization

```python
def fibo(n):
	global fibo_ls
    if n >= 2 and len(fibo_ls) <= n :
        fibo_ls.append(fibo(n-1)+fibo(n-2))
    return fibo_ls[n]
fibo_ls = [0,1]
```

- 이전에 계산한 값을 저장해두고, 다음 계산시 활용하는 기술
- 동적 계획법(DP)의 핵심 기술
  - 동적 계획 : 최적화 문제를 해결하는 알고리즘



## DP(Dynamic Programming)

```python
def fibo(n):
    fibo_ls=[0,1]
    
    for i in range(2,n+1):
        fibo_ls.append(fibo_ls[i-1] + fibo_ls[i-2])
```

- 작은 부분을 해결한뒤 그 값을 이용하여 큰 부분을 해결하는 형태의 알고리즘
- 재귀에 비해 함수 호출이 적어 성능면에서 효율적



## DFS(깊이 우선 탐색)

- 시작점에서부터 한 방향으로 갈 수 있는 곳까지 탐색하여 막히면 마지막 갈림길로 돌아가 탐색을 반복
- 가장 마지막 갈림길로 돌아가야 하므로 후입선출 구조의 스택이 사용됨

```python
#SWEA 1219
def tour(s):
    visit[s] = 1
    stack = [s]
    while True:
        if s == end:
            return 1
        visit[s] = 1
        for i in way[s]:						# 현재 지점에서 다른 지점 길 찾기
            if visit[i] == 0:					# 그 지점을 지나간적이 없으면
                s = i
                stack.append(s)
                break
        else:									# 갈 곳이 없으면 되돌아가기
            stack.pop()
            if not stack:						# 되돌아 갈 곳이 없으면 0
                return 0
            else:
                s = stack[-1]

for _ in range(10):
    tc,N = map(int,input().split())             # tc = 테스트케이스, N = 길의 총 개수
    target = list(map(int,input().split()))
    way = [[] for _ in range(100)]				# 지나 갈 수 있는 길을 표기
    visit = [0]*100								# 그 지점을 지나갔었는지 표기
    for i in range(N):
        a=target[i*2]
        b=target[i*2+1]
        way[a].append(b)
    start = 0
    end = 99
    print(f'#{tc} {tour(start)}')
```



## 백트래킹 (Backtracking)

- 답을 찾는 도중에 막히면 되돌아 가서 다시 답을 찾는 방법
- 노드를 점검 후 유망하지 않다면 다음 노드로 변경
- 최적화, 결정 문제를 해결 가능
  - 결정문제 : 조건을 만족하는게 존재 하는지 여부

### 백트래킹 <-> DFS

- 경로가 답으로 이어 질거 같지 않으면 그 경로를 포기 <-> 모든 경로를 추적
  - 불필요한 경로를 조기에 차단



## 분할 정복 알고리즘

- 분할-정복-통합으로 구분하여 구현
  - 분할:해결할 문제를 작은 부분으로 나눔
  - 정복: 나눈 문제를 각각 해결
  - 통합: 해결된 해답을 모음
- ex)거듭제곱

```python
# a**b
def exponent(a,b):
    basic = 1
    for i in range(b):
        basic *= a
    return basic
```

```python
def exponent(a,b):
    if b % 2 == 0 :
        root = exponent(a,b//2)
        return root * root
   	else:
        root = exponent(a,(b-1)//2)
        return root*root*a
```

