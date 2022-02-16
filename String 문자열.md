# String 문자열

## Brute Force

- 문자열을 처음부터 끝까지 차례대로 순회하면서 문자를 일일이 비교하는 방식

```python
find_str = 'ljm'
target = 'my name is ljm'
str_len = len(find_str)
target_len = len(target)

def Brute_force(find_str,target):
    i = 0 		#target 순회
    j = 0 		#find_str 순회
    while j < str_len and i < target_len :
        if target[i] != find_str[j]:		 #다음 시작점으로 이동
            i = i - j
            j -= 1
        i += 1
        j += 1
    if j == str_len :
        return i - str_len
    else:
        return -1
print(Brute_force(find_str,target))
#11 출력됨
```



## KMP 알고리즘

- 불일치가 발샌한 텍스트의 앞 부분 문자를 검사했으므로 불일치가 발생한 앞 부분에서 다시 시작하는 방법
- 찾고자 하는 문자의 패턴을 알아내어 다음 시작점을 찾음

```python
find_str = 'abcdabce'
target = ~~~~~~~abcdabcdabcef~~~~
#abc 패턴이 있음
#target에서 abc // d // abc // d에서 다름을 확인
#다음 확인 할 때 패턴에 따라 두번째 abc 지점에서 시작
```



## Boyer Moore (보이어-무어) 알고리즘

- 오른쪽에서 왼쪽으로 비교
- 오른쪽 끝에 있는 문자가 패턴 내에 존재하지 않아야함 

```python
find_str = 'ljm'
target = 'my name is ljm'
#target에서 찾을때 len(find_str)인 3간격으로 측정
#target[2] 확인, 확인결과 _<공백> find_str에 _이 없음 따라서 3칸 이동
#target[5] 확인, 확인결과 m // target[4]확인 결과 a, a는 find_str에 없음 //따라서 3칸 이동
#확인 결과 find_str이 존재할 경우 그 지점에서 find_str의 해당 문자를 놓고 좌우 비교
#비교시에도 끝 문자인 m부터 비교하여 반복 진행
```



## 암호

### 시저 암호

- 평문에서 사용되고 있는 알파벳을 일정한 문자 수 만큼 이동시켜 암호화
- Hello World 1만큼 이동
  - Ifmmp Xpsme

### bit열의 암호화

- 비트 연산의 배타적 논리합(exclusive_or) 사용 **XOR**



## 압축

### Run length encoding

- 같은 값의 반복을 압축
  - AAABCCCCLLJMM 압축시
    - A3B1C4L2J1M2
  - BMP 파일포맷 등에 사용됨

### Huffman coding

- 원본에서 자주 출현하는 문자는 적은 비트의 코드로 변환, 출현 빈도가 낮은 문자는 많은 비트의 코드로 변환
- LLLLLJJJMMMMA
  - L(5) , M(4), J(3),A(1)
  - 이진코드로 L을 00, M을 10, J를 11, A를 010 기록