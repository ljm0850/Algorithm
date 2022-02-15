# 배열 Array

- 시간 복잡도
  - 실제 걸리는 시간을 측정
  - 실행되는 명령문의 개수를 계산
  - 빅-O표기와 비슷(가장 큰 영향력을 주는 N에 대한 항만 표시)



## 정렬

### 버블 정렬(Bubble Sort)

- 첫 번째 원소부터 시작하여 **인접한 원소와 비교**하여 자리를 바꾸며 이동

- 시간복잡도 O(n^2)

```python
def Bubble_sort(bubble,N) : #정렬할 list, 원소 수
    for i in range(N-1,0,-1):
        for j in range(i):
            if bubble[j] > bubble[j+1]:
                bubble[j],bubble[j+1] = bubble[j+1],bubble[j]
```



### 카운팅 정렬(Conuting Sort)

- 각 **항목이 몇 개씩** 있는지 세는 작업을 하여 정렬

- 시간복잡도 O(n+k) : n=리스트길이,k=정수의 최대값

  ```python
  1.[0,1,1,3,3,3,9]
  2.[1,2,0,3,0,0,0,0,0,1] <0부터 9까지 몇개가 있는지(conut)>
  3.[1,3,3,6,6,6,6,6,6,7] <2번 list를 각 항목 앞에 위치할 항목의 개수 반영하기 위해 변경>
  #4번을 출력하면서 3번list의 값을 하나씩 줄임
  4.[0,1,1,3,3,3,9]
  ```

  ```python
  def Counting_sort(A,B,k): #A : 입력 배열(1~K), B:정렬된 배열, C:카운트배열,
      C = [0]*(K+1)
      
      for i in range(len(A)):
          C[A[i]] +=1
      for i in range(1,len(C)):
          C[i] += C[i-1]
      for i in range(len(B)-1,-1,-1):
          C[A[i]] -=1
          B[C[A[i]]] = A[i]
  ```




### 2차원 배열

- arr = [[0,1,2,3],[4,5,6,7]] 형식
- arr = [[0]*N for _ in range(N)]

	#### 배열순회

- n*m 배열의 모든 원소를 빠짐없이 조사하는 방법

  ```python
  for i in range(n):
      for j in range(m):
          arr[i][j] #행 우선 순회
          arr[j][i] #열 우선 순회
          arr[i][j + (m-1-2*j)*(i%2)] # 홀수,짝수번째일때마다 방향 바꿀때
  ```



#### 델타를 이용한 배열 탐색

- 2차 배열의 한 좌표에서 4방향의 인접 배열 요소 탐색

  ```python
  cnt = 1
  di = [0,1,0,-1] #우하좌상
  dj = [1,0,-1,0]
  now =[0,0]
  while cnt <= N :
          arr[now[0]][now[1]] = cnt
          now[0] += di[way]
          now[1] += dj[way]
          cnt += 1
  ```

  

#### 전치 행렬

- 대칭선(예시는 대각선)을 기준으로 반전

  ```python
  arr[[1,2,3][4,5,6][7,8,9]]
  
  for i in range(3):
      for j in range(3):
          if i < j : #i < j로 설정 안하면 다시 되돌아옴
              arr[i][j],arr[j][i] = arr[j][i], arr[i][j]
  ```



#### 부분집합

##### 비트 연산자

- `&`: 비트 단위로 AND 연산
- `|`: 비트 단위로 OR 연산(shift \\)
- `<<`: 피연산자의 비트 열을 왼쪽으로 이동
- `>>`: 피연산자의 비트 열을 오른쪽으로 이동

```python
i & (1<<j) : i의 j번째 비트가 1인지 아닌지를 검사
```

```python
arr = [1,2,3,4,5,6,7]
n = len(arr)

for i in range(1<<n):				# 1<<n : (2**n) 부분 집합의 개수
    for j in range(n):				# 원소의 수 만큼 비트를 비교
        if i & (1<<j):				# i의 j번 비트가 1인경우
            print(arr[j], end=","	# j번 원소 출력
```



### 순차 검색

- 일렬로 되어 있는 자료를 순서대로 검색
  - 간단하고 직관적
  - 검색 대상의 수가 많은 경우 수행시간이 증가하여 비효율적

#### 1. 정렬되어 있지 않은 경우

- **첫 번째 원소부터** 순서대로 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교,찾기
- 키 값이 동일하면 그 원소의 인덱스 반환

- 평균 비교 회수 = (n+1)/2,시간복잡도 O(n)

#### 2. 정렬되어 있는 경우

- 검색에 실패할 경우 평균 비교 횟수가 반으로 줄어듬
  - 찾고자 하는 값 < list값 일 경우 종료하면 되므로

##### 이진 검색(Binary Search)

- 자료의 **가운데**에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속
- 자료가 정렬되어 있어야함



### 선택 정렬

- 주어진 자료들 중 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식
- 정렬과정
  - 리스트에서 최소값 찾기
  - 그 값을 리스트 맨 앞에 위치한 값과 교환
  - 맨 처음 위치를 제외한 나머지 리스트를 대상으로 반복
- 시간복잡도 O(n**2)

```python
def Selection_sort(arr_ls,n):
    min_num = arr_ls[0]
    for i in range(0,n-1):
        #min_num = i
        #for j in range(i+1,n)
        #	if arr_ls[j] < arr_ls[min_num]:
        #   min_num = j 와 같이 최소값 찾기, 이때 최종min_num = k라고 할당
        arr_ls[i],arr_ls[k] =arr_ls[k],arr_ls[i]
```



### 셀렉션 알고리즘(Selection Algorithm)

- 저장 되어 있는 자료에서 k번째로 큰,작은 원소를 찾는 방법
- 과정
  - 정렬 알고리즘을 이용하여 자료 정렬
  - 원하는 순서에 있는 원소 가져오기
- 교환의 회수가 버블,삽입 정렬보다 작다

```python
def Select(arr,k):
    for i in range(0,k):
        min_index = i
        for j in range(i+1,len(arr)):
            if arr[min_index] > arr[j]:
                min_index = j
        arr[i],arr[min_index] = arr[min_index],arr[i]
    return arr[k-1]       
```

