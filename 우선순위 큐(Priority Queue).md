# 우선순위 큐(Priority Queue)

- 우선순위가 가장 높은 데이터가 먼저 나갈 수 있는 형태의 자료구조
- 삽입,삭제,탐색에 O(logN)
- python에선 PriorityQueue 라는 class가 있지만, thread간의 synchronized를 맞춰야 해서 속도가 느림
  - `heapq`사용
  - https://docs.python.org/ko/3/library/heapq.html
- 언어마다 우선순위가 다름
  - python,java의 경우 숫자가 작을수록 우선 순위가 높음
  - cpp의 경우 숫자가 클수록 우선 순위가 높음

```python
# nums에서 가장 큰 수를 빼서 -1 하는 것을 m번 반복한 뒤 최대값을 구하는 문제
# import heapq
from heapq import heappush,heappop
import sys

n,m = map(int,sys.stdin.readline().split())
nums = list(map(int,sys.stdin.readline().split()))
heap = []
for num in nums:
    heappush(heap,-num)

for _ in range(m):
    max_num = heappop(heap)
    heappush(heap,max_num+1)
ans = -heappop(heap)
print(ans)
```

