# 정수론(Number Theory)

## 모듈러 연산

- (a+b)%c == (a%c+b%c)%c

```python
7%3 == 1
8%3 == 2
(7+8)%3 == 0
(7%3+8%3)%3 == 0
```

```python
number = ac + d
number//c == a
number%c == d

A = ac + x
B = bc + y
A+B = (a+b)c + (x+y)
```

- **정리**

```python
(a+b) % c == (a%c + b%c) % c
(a-b) % c == (a%c - b%c + c) % c 		# +c해주는 것은 a%c-b%c가 음수가 되는것을 방지 
(a*b) % c == (a%c * b%c) % c

```

- 모듈러 나눗셈

```python
(a/b) % c = (a*(b**-1))%c = (a*c)*((b**-1)%c)%c	
```

1. (b**-1)%c가 문제
2. 페르마의 소정리, 유클리드 호제법을 이용하여 역원을 구하여 계산은 가능



## 소수 찾기

- 완전탐색

  ```python
  n = int(input)		#n이 소수인가 아닌가 판별
  cnt = 0
  
  for i in range(1,n+1):
      if n%i == 0:
          cnt +=1
  if cnt == 2:
      print('prime number')
  else:
      print('False')
  ```

- 약수는 항상 짝이 있음을 이용, 루트n까지만 계산(루트n 이상의 약수는 이전에 다른 약수와 짝이 됬으므로)

  ```python
  n = int(input())
  
  cnt = 0
  for i in range(1,n+1):
      if i**2 >n:				#루트n까지만 검색하면 모두 탐색, 루트보단 제곱이 정확해서 제곱으로
          break
      if n%i == 0:
          cnt +=1
          
  if cnt == 2:
      print('prime number')
  else:
      print('False')
  ```



## 소인수 분해

- 완전탐색

  ```python
  n = int(input())
  prime_number=[]
  for i in range(2,n+1):
      while n % i == 0:
          prime_number.append(i)
          n //= i        
  ```

  

- 소수찾기에서 쓰인 방식 활용

  ```python
  n = int(input())
  prime_factor=[]
  
  a = n							#원본이 변현되는걸 막기 위해(break문)
  for i in range(2,n+1):
      if i*i > n:
          break
      while a % i == 0:
          prime_factor.append(i)
          a //= i
  if x != 1:
      prime_factor.append(x)
  ```

  

## 약수 구하기

- 완전탐색

  ```python
  n = int(input())
  prime = []
  
  for i in range(1,n+1):
      if n % i == 0:
          prime.append(i)
  ```

- 약수 짝을 이용

  ```python
  n = int(input())
  prime = []
  
  for i in range(1,n+1):
      if i**2 > n:
          break
  	if n % i == 0:
          prime.append(i)
          if i**2 != n:					#루트n이 정수일경우 약수에 루트n이 두번들어가는것 방지
              prime.append(n//i)
  ```

  