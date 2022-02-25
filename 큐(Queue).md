# 큐(Queue)

- 뒤에서는 값을 추가만 하고, 앞에서는 삭제만 하는 구조
- 선입선출 구조(FIFO:First In First Out)
  - 들어온 순서대로 삭제됨

### 주요 연산

- enQueue(item)
  - 큐의 뒤쪽에 원소(item)를 추가하는 연산

- deQueue()
  - 큐의 앞쪽 원소를 삭제하고 반환하는 연산
- createQueue()
  - 공백 상태의 큐를 생성하는 연산
- isEmpty()
  - 큐가 공백상태인지를 확인하는 연산
- isFull()
  - 큐가 포화상태인지를 확인하는 연산
- Qpeek()
  - 큐의 맨앞 원소를 삭제없이 반환만 하는 연산

## 선형 큐

```python
#선형 큐 만들어봄
class Queue:
    def __init__(self,size):
        self.size = size					#배열의 크기
        self.front = -1						#첫 원소의 인덱스(머리부분)
        self.rear = -1						#마지막 원소의 인덱스(꼬리부분)
        self.items = [None] * self.size

    def enQueue(self,item):
        if self.isFull() : print('Queue_Full')
        else:
            self.rear += 1
            self.items[self.rear] = item

    def deQueue(self):
        if self.isEmpty() : print('Queue_Empty')
        else:
            self.front += 1
            return self.items[self.front]

    def isEmpty(self):
        return self.front == self.rear

    def isFull(self):
        return self.rear == self.size -1

    def Qpeek(self):
        if self.isEmpty() : print('Queue Empty')
        else:
            return self.items[self.front+1]
```

- item 추가,삭제를 반복할 경우 앞에 공간이 비어 있어도 활용이 불가
  - 삭제가 될때마다 앞부분으로 이동하는 방법
    - 이동에 시간이 걸려 효율성이 떨어짐
  - 원형 큐 사용(size를 넘어서게 되면 앞으로 되돌아가서 앞에서부터 덮어 씌움)

## 원형 큐

- front, rear 모두 0부터 시작
- front,rear 이 n-1 도착시 그다음 작업시 0으로 이동 (나머지 연산자 mod(%)사용)
  - **enQueue**에서 rear = (rear+1) % size
  - **deQueue**에서 front = (front+1) % size
  - **isFull**에서 (rear+1) % size == front 로 변경





## 우선순위 큐(Priority Queue)

- 선입선출 순서가 아닌 우선 순위로 나가게 된다

- 배열을 이용하여 구현
  - 원소를 삽입하는 과정에서 우선순위를 비교하여 우선순위에 따라 다르게 삽입
  - 삽입,삭제 연산에 원소의 재배치로 인해 시간,메모리 낭비가 큼



## 버퍼(Buffer)

- 데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 데이터를 보관하는 메모리 영역
- 먼저 입력한 순서대로 데이터를 보내야 하므로 선입선출 방식인 큐가 활용됨



## BFS(Breadth First Search)

- 그래프 탐색 방법중 한가지
  - DFS (깊이 우선 탐색)
  - BFS (너비 우선 탐색)

- 시작점의 인접한 곳을 탐색한 후, 차례로 시작점의 인접한곳의 인접한곳 탐색 하는 형식
  - 중복 탐색을 막기 위해 DFS와 같이 검색한곳을 check하는 list(viseted 만들던거)를 만들어서 자주 사용