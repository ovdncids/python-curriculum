# Python

## 변수 (Variable)
### 변수를 사용하는 이유
1. 자료형 데이터를 보관 할 수 있고, 자유롭게 값을 수정 할 수 있다.

variable.py
```py
// 변수 Create
v1 = True
v2 = 100
v3 = 'abc'

// 변수 Read
print(v1, v2, v3)

// 변수 Update
v1 = False
v2 = -10
v3 = 'def'

// 변수 Read
print(v1, v2, v3)
```
* 자료형에는 `Boolean`(True, False), `Number`(숫자), `String`(문자) 3가지가 주로 쓰인다.
* 변수 선언문이 다른언어와 다른점 설명
* `print();` 설명
* ❔ 선언 하지 않은 `v4` 변수를 `print(v4)`로 찍는다면
* `변수`에 대한 `CRUD` 설명
* ❕ `변수명`에 대한 규칙
  ```
  제어문 이름으로 사용 불가 (if, for, switch, while, ...)
  연산자 이름으로 사용 불가 (+, -, *, /, ==, !, <, >, this, ...)
  자료형 또는 예약어(명령어) 사용 불가 (True, False, None, ...)
  숫자를 앞으로 사용 불가 (1a, 2b, ...)
  영문, _, 숫자 조합으로 사용 (_a, b1, c_1, ...)
  대소문자 구분 (low_UP, Low_Up, LOW_UP)
  주로 `snake_case(스네이크) 표기법`으로 사용 (car_use, bus_take, ...)
  ```

2. `디버깅 모드`에서 연산의 과정을 볼 수 있다.
```py
print(1 + 2 + 3)
num1 = 1
num2 = 2
num3 = 3
sum1 = num1 + num2
sum2 = sum1 + num3
print(sum2)
```
* breakpoint 설명

3. 변수 수정으로 프로그램 전체를 수정 가능하다.
```py
calc = 100
print(calc + 10)
print(calc - 10)
print(calc * 10)
print(calc / 10)
```
* ❔ 변수 `calc` 값 수정해 보기

### 한줄에 변수 여러개 선언하기 (선언문)
```py
a = 1, b = 2, c = 3
print(a, b, c)
```
* ❔ 문제: 한줄로 변수 `a, b, c`에 각각 `1, 2, 3` 넣어 보기
* <details><summary>정답</summary>

  ```py
  a, b, c = 1, 2, 3
  ```
</details>

## 상수 (Constant)
### 상수를 사용하는 이유
1. 한번 선언된 값의 변경을 막기 위해 사용 한다.
* <details><summary>설명</summary>

  ```
  하지만 python은 상수가 없다
  ```
</details>

## 연산자 (Operator)
operator.py

1. 문자에 대한 사칙 연산자 (`+, -, *, /`)
```py
type1 = 1
type2 = 2
result1 = type1 + type2
result2 = type1 - type2
result3 = type1 * type2
result4 = type1 / type2
print(result1, result2, result3, result4)
```
* ❔ `type1` 값을 숫자 True로 바꾼다면
* ❔ `type1` 값을 숫자 False로 바꾼다면
* ❔ `type1` 값을 '1'로 바꾼다면
* ❕ int 함수 적용
* ❔ `type2` 값을 '2'로 바꾼다면
* ❕ `type2` 값을 2로 바꾼다면 후 str 함수 적용
* ❔ 문제: 다음의 `r` 값이 '21a'를 만들기 위해, int 또는 str 함수를 적용
  ```py
  r = 2 + '1' + 'a'
  ```
* <details><summary>정답</summary>

  ```py
  r = str(2) + '1' + 'a'
  ```
</details>

* ❔ 문제: 프리랜서 개발자가 월 500만원을 받고 있다. 3.3% 원천징수를 때고 받는 실수령액과 세금을 계산하라.
  ```py
  salary = 5000000
  rate = 3.3
  tax = ??
  realSalary = ??

  힌트: 세금 계산식 = 급여 * 원천징수 / 100
  ```
* <details><summary>정답</summary>

  ```py
  salary = 5000000
  rate = 3.3
  tax = salary * rate / 100
  realSalary = salary - tax
  print(tax, realSalary)
  ```
</details>

2. ==(동등 연산자) 연산자
```py
oNum1 = 1 == '1'
True1 = 1 == True
True2 = 1 != True
False1 = 0 == False
False2 = 0 != False
char1 = True == 'True'
print(oNum1, True1, True2, False1, False2, char1)
```
* ❕ 연산이 끝나면 `Boolean` 형식으로 결과를 반환한다.
* ❔ 문제: `1`과 `2`를 `동등 연산자`로 비교 후에 변수 `x`에 넣고, `x`를 `print`로 찍어 보기
* <details><summary>정답</summary>

  ```py
  x = 1 === 2
  print(x)
  ```
</details>

3. 비교 연산자 (<, <=, >, >=)
```py
compare1 = 1 < 1
compare2 = 2 <= 2
compare3 = 3 > 3
compare4 = 4 >= 4
print(compare1, compare2, compare3, compare4)
```

4. 논리 연산자 (and, or)
```py
logical1 = True and True
logical2 = False or False
print(logical1, logical2)
```
* `and`를 사용하는 상황: 로그인이 되어 있고, 글수정 권한이 있는 아이디인 경우, 글수정 버튼 활성화
* `or`를 사용하는 상황: 프리미엄 회원이거나 광고를 본 경우, 영상 시청 가능

5. 소괄호() 연산자
```py
roundBracket1 = 1 + 2 * 3
roundBracket2 = (1 + 2) * 3
roundBracket3 = ((1 + 2) * 3)
print(roundBracket1, roundBracket2, roundBracket3)
```
* ❕ `소괄호 연산자`는 `사칙 연산자`보다 우선 순위를 갖는다.
* ❔ 문제: `소괄호 연산자` 안에서 `True`와 `False`를 `동일 연산자`로 연산 후에 변수 `y`에 넣고, `y`를 `print`로 찍어 보기
* <details><summary>정답</summary>

  ```py
  y = (True == False)
  print(y)
  ```
</details>

## if문(제어문 > 조건문)
1. 기본 구조
```py
if (조건1):
  # 조건1이 참인 경우 실행
elif (조건2):
  # 조건2가 참인 경우 실행
elif (조건3):
  # 조건3이 참인 경우 실행
  # else if는 여러게 사용 가능
else:
  # 해당 되는 조건이 없을 경우 실행
```
* 예제
```py
if1 = 1
if (if1 == 1):
  print('참1')
elif (if1 == 2 or if1 == 3):
  print('참2 또는 참3')
elif (if1 == 4 and True):
  print('참4')
else:
  print('거짓')
```
* 조건은 주로 연산자를 사용해서 `Boolean` 형식으로 받는다.
* `if1` 값을 수정하여 `참2 또는 참3`이 나오게 만들기
* `if1` 값을 수정하여 `참4`이 나오게 만들기
* `if1` 값을 수정하여 `거짓`이 나오게 만들기

2. 거짓 조건 비교 하기
* ❕ 거짓 조건은 `False`, `0`, `None`, `''` 이고, 나머지는 모두 참인 조건이 된다.
```py
d1 = False
d2 = None
condition1 = d1 == d2
condition2 = False
if (condition2):
  print('참')
else:
  print('거짓')
```
* ❔ 문제: 조건이 `1 == 1`인 `if`문을 만들고, 참인 경우 `print('참');`을 찍어 보기
* <details><summary>정답</summary>

  ```py
  if (1 == 1):
    print('참')
  ```
</details>

### 3항 연산자
```py
condition3 = 'a' if 1 == 1 else 'b'
print(condition3)
```
* ❔ 문제: 조건이 `2 == 3`인 `3항 연산자`문을 만들고, 참인 경우 `'c'` 거짓인 경우 `'d'`를 `condition4` 상수에 넣어 보기
* <details><summary>정답</summary>

  ```py
  condition4 = 'c' if 2 == 3 else'd'
  print(condition4)
  ```
</details>

## 배열
### 배열을 사용하는 이유
1. 순차적인 반복 작업에 사용한다. (주로 동일한 데이터 타입으로 묶인 경우가 많다.)
2. 숫자(index)를 바탕으로 해당 데이터에 접근 한다.

### 배열 선언
array.py
```py
array1 = []
array2 = [1, 2, 3]
print(array1, array2)
```
https://t1.daumcdn.net/blogfile/fs8/27_25_21_25_0O7Ul_IMAGE_0_42.jpg?original&filename=42.jpg

### 배열의 CRUD
```py
// 배열 Create
array1.append(1)
array1.append('2')
array1.append('삼')

// 배열 Read
array1[0]
a1 = array1[0]
a2 = array1[1]
a3 = array1[2]

// 배열 Update
array1[0] = None
array1[1] = False
array1[2] = [1, 2, 3]

// 배열 Delete
array1.remove(array1[0])
array1.remove(array1[1])
array1.remove(array1[2])
```
* ❔ `Python Console 창`에서 `배열의 CRUD` 실행 해보기 (터미널에서 `python` 실행)

### 배열의 크기
```py
length1 = len(array1)
length2 = len(array2)
lastIndex = len(array2) - 1
lastValue = array2[lastIndex]
print(lastIndex, lastValue)
```
* ❕ `lastValue`는 `array2` 배열의 마지막 요소의 값을 받는다.

### 배열의 성격
```py
arr1 = []
arr2 = []
# quiz1
if (arr1):
  result = '참'
  print(result)
else:
  result = '거짓'
  print(result)

quiz2 = arr1 == arr2
quiz3 = arr1 is arr2
quiz4 = arr1[5]
#quiz5
arr1[9] = 10
```
* ❔ `빈 배열`은 참일까 거짓일까?
* ❔ 문제: `arr1`와 `arr2`는 같을까?
* <details><summary>정답</summary>

  https://ovdncids.github.io/javascript-curriculum/images/memory.png
  ```
  배열은 선언과 동시에 별도의 `메모리 공간`에 존재하고, 변수는 단지 해당 배열이 있는 `메모리 주소`를 가지고 있다.
  따라서 `arr1`과 `arr2`는 서로 다른 배열의 주소를 가지므로 같지 않다.
  만약 `arr1` 변수의 값을 변화 시킨다면, `메모리 주소`를 잃어 버리므로 해당 배열은 더이상 접근할 수 없게 된다.
  ```
</details>

* ❔ 해당 배열이 가진 `len`보다 큰 `index`를 `Read` 한다면?
* ❔ 해당 배열이 가진 `len`보다 큰 `index`를 `Update` 한다면?

### 익명 배열
```py
print([1, 2, 3])
```
* 해당 배열의 `메모리 주소`를 누구도 받지 않으므로 재사용 할 수 없다.

### 배열 실습
* 1 부터 5까지 더하기(total 변수를 만들어서 한번씩 더해서 만듬)
```py
testArray1 = [1, 2, 3, 4, 5]
total1 = testArray1[0]
total1 = total1 + testArray1[1]
total1 = total1 + testArray1[2]
total1 += testArray1[3]
total1 += testArray1[4]
print(total1)
```

* `testArray1` 평균 구하기
```py
avg = total1 / len(testArray1)
print(avg)
```

* `testArray1` 홀수만 더하기
```py
odd1 = testArray1[0] + testArray1[2] + testArray1[4]
print(odd1)
```

* `testArray1` 짝수만 더하기
```py
even1 = testArray1[1] + testArray1[3]
print(even1)
```

* 홀수만 지우기
```py
testArray1.remove(testArray1[0])
testArray1.remove(testArray1[1])
testArray1.remove(testArray1[2])
print(testArray1)
```

## for문(제어문 > 반복문)
### for문을 사용하는 이유
1. 반복 작업을 한곳으로 묶기 위해 사용함 (주로 배열이 사용 된다.)
2. 주로 게시판에 목록을 보여줄때 주로 사용함

### for문 문법
for.py
1. 기본 구조
```py
for 증가변수 in [문자 또는 배열 또는 객체]:
  실행문
```
* 예제
```py
for index1 in range(0, 5):
  print(index1)

# list1 = list(range(0, 5))
# print(list1)
# print(index1)
```

2. break
```py
for index2 in range(0, 5):
  print(index2)
  break
```

3. continue
```py
for index3 in range(0, 5):
  if index3 == 2:
    continue
  print(index3)
```

### 홀수와 짝수 표현하기
```py
for index4 in range(1, 11):
  if index4 % 2 == 1:
    print('숫자 ' + str(index4) + '은 홀수 입니다.')
  else:
    print('숫자 ' + str(index4) + '은 짝수 입니다.')
  # oddEven = '홀수' if index4 % 2 else '짝수'
  # print('숫자 ' + str(index4) + '은 '+ oddEven + ' 입니다.')
```

### 총합 더하기
```py
total1 = 0
for index4 in range(1, 6):
  total1 = total1 + index4
  # total1 += index4
  print(total1)

print(total1, index4)
```
* ❔ `total1 = 0`을 주석 처리 한다면
* VSCode에서 `index4`, `total1` 마우스 오버해보기, Ctrl(또는 command) 키를 눌러서 해당 변수 이동)

* ❔ 문제: `total1`의 `평균` 값을 구해 `avg1` 변수에 넣고, `avg1`을 `print`로 찍어 보기
* <details><summary>정답</summary>

  ```py
  avg1 = total1 / index4
  print(avg1)
  ```
  `total1 / 5 ` 이렇게 바로 나누었다면, 나중에 프로그램이 1에서 10까지로 변한다면, `5`값을 `2군데`에서 수정 해야 한다.
</details>

### for문에서 배열 사용하기
```py
array1 = [1, 2, 3]
for index5 in array1:
  print(index5)

print(index5)
```
* ❔ 문제: `array2 변수`에 `빈 배열`을 넣고, 위에 for문을 이용해 `array2` 배열을 `[1, 2, 3]`으로 만들고, `array2`를 for문이 끝나고 `print`로 찍어 보기
* <details><summary>정답</summary>

  ```py
  array1 = [1, 2, 3]
  array2 = []
  for index6 in array1:
    array2.append(index6)

  print(array2)
  ```
</details>

* ❕ 결과적으로 `array2`는 `array1`을 복사하였다.
* ❔ `array1 is array2` 참일까요?
* ❕ 메모리 설명
```py
array3 = [1, 2, 3]
array4 = array3
```
* ❔ `array3 is array4` 참일까?
```py
array3 = 3
array4 = 4
```
* ❔ 문제: `array3`에서 사용하던 배열에 다시 접근할 수 있을까?
* <details><summary>정답</summary>

  없다. (배열은 `상수`를 사용 하면 안전 하지만, `Python`은 상수를 지원하지 않는다)
</details>

### index++와 ++index의 차이
```py
index = 0
diff1 = index++
diff2 = ++index
```
* ❕ `Python`은 증감 연산자를 지원하지 않는다
