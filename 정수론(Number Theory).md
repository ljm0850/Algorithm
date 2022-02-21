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



## 에라토스테네스의 체

- 소수를 찾는 방법중 하나

- 2부터 소수를 구하고자 하는 구간의 모든 수를 나열

- 첫번째 소수 2를 구함, 2의 배수 제거

- 두번째 소수 3을 구함, 3의 배수 제거

- 세번째 소수 5를 구함, 5의 배수 제거

- 구한소수**2 > 범위최대가 될떄까지 ...반복

  

```python
def prime_list(n):
    # 에라토스테네스의 체 초기화: n개 요소에 True 설정(소수로 간주)
    sieve = [True] * n

    # n의 최대 약수가 sqrt(n) 이하이므로 i=sqrt(n)까지 검사
    m = int(n ** 0.5)
    for i in range(2, m + 1):
        if sieve[i] == True:           # i가 소수인 경우
            for j in range(i+i, n, i): # i이후 i의 배수들을 False 판정
                sieve[j] = False

    # 소수 목록 산출
    return [i for i in range(2, n) if sieve[i] == True]

#출처 https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4
```

------

#### n! 에 곱해진 소수

```python
n = int(input())		#n!
p = int(input())		#소수

cnt = 0					#소수가 몇번 곱해졌는지
a=p						#while문 조건 변경 방지
while a <= n:
    cnt += n//a			# 1부터 n까지의 a값의 배수의 개수 추가
    a *= p				# p제곱으로 다시 검사 시작 
```

