# Python

## 변수 (Variable)
### 변수를 사용하는 이유
1. 자료형 데이터를 보관 할 수 있고, 자유롭게 값을 수정 할 수 있다.

variable.py
```py
# 변수 Create
v1 = True
v2 = 100
v3 = 'abc'

# 변수 Read
print(v1, v2, v3)

# 변수 Update
v1 = False
v2 = -10
v3 = 'def'

# 변수 Read
print(v1, v2, v3)
```
* 자료형에는 `Boolean`(True, False), `Number`(숫자), `String`(문자) 3가지가 주로 쓰인다.
* 변수 선언문이 다른언어와 다른점 설명
* `print();` 설명
* ❔ 선언 하지 않은 `v4` 변수를 `print(v4)`로 읽는(Read)다면
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
* ❕ `True and True`를 `True and 1`으로 바꾼다면
* ❕ `False or False`를 `False or 'a'`으로 바꾼다면
* ❕ `논리 연산자`는 주로 `if문` 안에서 사용

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
# 배열 Create
array1.append(1)
array1.append('2')
array1.append('삼')

# 배열 Read
array1[0]
a1 = array1[0]
a2 = array1[1]
a3 = array1[2]

# 배열 Update
array1[0] = None
array1[1] = False
array1[2] = [1, 2, 3]

# 배열 Delete
del array1[0]
del array1[1]
del array1[2]
```
<!--
array1.remove(array1[0])
-->
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
* 1부터 5까지 더하기(total 변수를 만들어서 한번씩 더해서 만듬)
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

* ❔ 문제: 짝수만 지우기

## for문(제어문 > 반복문)
### for문을 사용하는 이유
1. 반복 작업을 한곳으로 묶기 위해 사용함 (주로 배열이 사용 된다.)
2. 주로 게시판에 목록을 보여줄때 주로 사용함

### for문 문법
for.py
1. 기본 구조
```py
for 증가변수 in [문자 또는 배열 또는 (딕셔너리 객체)]:
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
  # print('숫자 ' + str(index4) + '은 ' + oddEven + ' 입니다.')
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
  `total1 / 5` 이렇게 바로 나누었다면, 나중에 프로그램이 1에서 10까지로 변한다면, `5`값을 `2군데`에서 수정 해야 한다.
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
* ❔ `array1 is array2` 참일까?
* ❕ 메모리 설명
```py
array3 = [1, 2, 3]
array4 = array3
```
* ❔ 문제: `array3 is array4` 참일까?
* <details><summary>정답</summary>

  ```py
  print(id(array3))
  print(id(array4))
  ```
  메모리 주소값이 같아서 `array3`과 `array4`는 서로 같다.
</details>

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

## 함수
### 함수를 사용하는 이유
1. 주로 버튼을 클릭후 동작을 `함수`에 정의 한다.
2. 여러줄에 걸쳐 실행되던 동일한 작업을, 함수 호출 한줄로 동일한 결과를 만들어 낼 수 있다. (반복됐던 만큼 코드양이 줄어 가독성을 높일 수 있다.)
* `DRY`: (Don't repeat yourself)
* 동일한 작업이 `2번 이상 반복` 된다면 무조건 함수로 만든다. (이런 작업을 `리팩토링`이라 한다.)

### 함수 문법
function.py
1. 기본 구조
```py
# 함수 선언부
def 함수명(인자1, 인자2, ...):
  실행문
  ...
  return 반환값

# 함수 호출부
반환받는상수 = 함수명(인수1, 인수2, ...)
```

* 예제
```py
def func1(parameter1, parameter2):
  sum1 = parameter1 + parameter2
  return sum1

print(func1)
returned1 = func1('argument1', 'argument2')
print(returned1)
```
* `breakpoint`로 진행 확인
* `실행`과 `호출`의 차이 설명하기
* `func1(1, 2)` `호출` 해보기
* ❔ 함수 안에 `return`이 없다면 `returned1`의 값은?
* ❔ `argument2`를 넘기지 않는다면?
* `parameter1`은 함수 내부적으로 `parameter1 = 인수1` 이렇게 작동 한다.
* ❔ `parameter2`를 지운다면?
* ❔ 문제: `print('함수 호출')`이라는 실행문을 가진 `함수` `f1`을 만들고, 해당 `함수` 호출 시키기
* <details><summary>정답</summary>

  ```py
  def f1():
    print('함수 호출')
  f1()
  ```
</details>

2. 인수에 자료형 데이터 넘기기
```py
v1 = 'a'
def func2(parameter1):
  compare1 = v1 == parameter1
  parameter1 = 'b'
  compare2 = v1 == parameter1
  print(compare1, compare2)

func2(v1)
```
* ❔ `compare1`, `compare2`는 `참`일까, `거짓`일까?

3. 인수에 배열 넘기기
```py
v2 = []
def func3(parameter1):
  compare1 = v2 == parameter1
  compare2 = v2 is parameter1
  parameter1.append('a')
  v2.append('b')
  compare3 = v2 == parameter1
  compare4 = v2 is parameter1
  print(compare1, compare2, compare3, compare4)

func3(v2)
```
* ❔ `compare1`, `compare2`, `compare3`, `compare4`는 `참`일까, `거짓`일까?

4. 인수에 함수 넘기기
```py
def v3():
  print('v3')

def v4():
  print('v4')

def func4(parameter1):
  compare1 = v3 == parameter1
  compare2 = v3 is parameter1
  parameter1 = v4
  compare3 = v3 == parameter1
  compare4 = v3 is parameter1
  parameter1 = v3
  compare5 = v3 == parameter1
  compare6 = v3 is parameter1
  print(compare1, compare2, compare3, compare4, compare5, compare6)

func4(v3)

```
* ❔ `compare1`, `compare2`, `compare3`, `compare4`, `compare5`, `compare6`는 `참`일까, `거짓`일까?

5. 익명 함수
```py
func5 = lambda x: x
v5 = func5(123)
print(v5)
```
* 익명 함수를 인수로 넘기기
```py
def func6(parameter1):
  print(parameter1)
  # 익명함수 호출

func6(lambda: print('abc'))
```
* ❔ 문제: `인수`로 넘긴 `익명 함수`를, `인자`로 호출 시키기
* <details><summary>정답</summary>

  ```py
  parameter1()
  # 인수로 함수를 넘기고, 인자로 호출시키는 함수를 `콜백 함수`(Callback function)라 한다.
  ```
</details>

6. 라이브러리: 특정 함수들의 모음 (calendar, random)
```py
import calendar
print(calendar.calendar(2015))

import random
print(random.random())
```

### 함수 실습 (회원 CRUD 만들기)
membersFunction.py
```py
members = []

# Create
def membersCreate(member):
  members.append(member)
  return members

# Read
def membersRead():
  return members

# Delete
def membersDelete(index):
  members.remove(members[index])
  return members

# Update
def membersUpdate(index, member):
  members[index] = member
  return members
```

```py
# Create
membersCreate('홍길동')

# Read
membersRead()

# Update
membersUpdate(0, '김유신')

# Delete
membersDelete(0)
```

* `Python Console 창`에서 실행
```py
import membersFunction

membersFunction
membersFunction.members

membersCreate = membersFunction.membersCreate
membersRead = membersFunction.membersRead
membersUpdate = membersFunction.membersUpdate
membersDelete = membersFunction.membersDelete
```

* `배열의 CRUD`를 참조 하여, `membersFunction2.py` 파일을 생성하고, 처음 부터 코딩 해보기

## 오브젝트 (딕셔너리 객체)
### 오브젝트를 사용하는 이유
1. 효율적인 관리를 위해 여러 변수를 한곳에 묶어서 사용한다.

### 배열과 오브젝트의 차이점
* ❕ 배열은 숫자(index)로 요소에 접근하고, 오브젝트는 문자(key)로 요소에 접근한다.

### 오브젝트 문법
object.py
1. 기본 구조
```py
오브젝트명 = {
  '키1': 값1,
  '키2': 값2  
}
```

https://ovdncids.github.io/javascript-curriculum/images/object.jpeg

* 예제
```py
def func7():
  print(object1, object2)

object1 = {}
object2 = {
  'key1': '값1',
  'key2': [1, 2, 3],
  'key3': func7,
  'key4': {
    'k1': 'v1',
    'k2': 'v2'
  }
}
```

### 오브젝트의 CRUD
```py
# 오브젝트 Create
object1['key1'] = 1
object1['key2'] = '2'
object1['key3'] = '삼'

# 오브젝트 Read
object1['key1']
o1 = object1['key1']
o2 = object1['key2']
o3 = object1['key3']

# 오브젝트 Update
object1['key1'] = []
object1['key2'] = func7
object1['key3'] = {
  'k1': 'v1',
  'k2': 'v2'
}

# 오브젝트 Delete
del object1['key1']
del object1['key2']
del object1['key3']

print(object1)
```

#### `Python Console 창`에서 `오브젝트의 CRUD` 호출 해보기
```py
import object

object
object1 = object.object1
object2 = object.object2
```

* 좀더 쉽게 가져오는 방법
```py
from object import object1, object2
```

#### `object2` 활용
* ❔ `object2['key2']` 배열의 `length` 구하기
* ❔ `object2['key3']` 함수 호출 시키기
* ❔ `object2['key4']` 오브젝트의 `k1`키 삭제 하기
* ❔ `object2['key5']` 선언 되지 않은 `key5` 읽기

* ❕ `키`이름에 대한 규칙
```
키는 문자로 받아서 자유롭게 조합이 가능하다
```

### 오브젝트의 for in문
```py
for v1 in object2:
  value1 = object2[v1]
  print(v1)
  print(value1)
  print(object2['v1'])
```

### Object의 멤버 변수의 수 구하기
```py
count = leng(object2)
print(count)
```

### 오브젝트 실습 (회원 CRUD 사용)
* `Python Console 창`에서 `회원 CRUD` 호출 해보기
```py
from membersFunction import membersCreate, membersRead, membersUpdate, membersDelete
```
```py
# Create
membersCreate({
  'name': '홍길동',
  'age': 20
})

# Read
membersRead()

# Update
membersUpdate(0, {
  'name': '김유신',
  'age': 30
})

# Delete
membersDelete(0)
```
* `회원 CRUD` 안보고 Console 창에서 CRUD 호출 해보기

## 클래스
### 클래스를 사용하는 이유
1. `인스턴스 오브젝트`를 만들기 위해서 `클래스`를 생성한다.
2. 오브젝트는 `붕어빵`, 클래스는 `붕어빵 기계`라고 생각하면 쉽다. (붕어빵 기계 하나가 하루에 100개 이상의 붕어빵을 만들수 있다.)

### 클래스 문법
class.py

1. 기본 구조
```py
class 클래스명:
  키1 = 값1
  키2 = 값2
}
```

* 예제
```py
class Class1:
  pass

class Class2:
  key1 = '값1'
  key2 = [1, 2, 3]
  def key3(self):
    print(self.key1)
  key4 = {
    'k1': 'v1',
    'k2': 'v2'
  }

object1 = Class1()
object2 = Class2()
```
* `pass`는 `class문` 안에 내용이 없을때 사용한다.

### 오브젝트의 CRUD
```py
# 오브젝트 Create
object1.key1 = 1
object1.key2 = '2'
object1.key3 = '삼'

# 오브젝트 Read
object1.key1
o1 = object1.key1
o2 = object1.key2
o3 = object1.key3

# 오브젝트 Update
object1.key1 = []
object1.key2 = object2.key3
object1.key3 = {
  'k1': 'v1',
  'k2': 'v2'
}

# 오브젝트 Delete
del object1.key1
del object1.key2
del object1.key3

print(object1)
```

#### `Python Console 창`에서 `오브젝트의 CRUD` 호출 해보기
```py
from class import object1, object2
```

#### `object2` 활용
* ❔ `object2.key2` 배열의 `length` 구하기
* ❔ `object2.key3` 함수 호출 시키기
* ❔ `object2.key4` 오브젝트의 `k1`키 삭제 하기
<!--
`del object2.key3` 삭제 할때 에러가 발생할 경우
`object2.key3 = None` 먼저 실행 후 삭제 한다.
-->
* ❔ `object2.key5` 선언 되지 않은 `key5` 읽기

* ❕ `키`이름에 대한 규칙
```
`영문, 숫자, _`를 자유롭게 조합해서 쓸 수 있다.
숫자를 앞으로 사용 불가 (1a, 2b, ...)
```

<!--
for in 문 안됨 (How to make a class Iterable & create Iterator Class for it)
* https://thispointer.com/python-how-to-make-a-class-iterable-create-iterator-class-for-it
* https://goodthings4me.tistory.com/58
Class는 전체 멤버에 대한 Iterate는 지원 하지 않지만, 하나의 멤버에 대해서는 __iter__, __next__ 사용해서 만들 수 있다.
-->

## try catch문(제어문 > 예외처리문)
### try catch문을 사용하는 이유?
1. 에러가 발생할 경우 처리를 위해 사용한다.
2. try문 밖에서 에러가 발생할 경우 프로그램 진행이 멈추지만, try문 안에서 발생할 경우 프로그램이 계속 진행 된다.

* 기본 구조
```py
try:
  실행문
  ...
except Exception as 에러객체:
  # try block에서 에러가 발생할 경우 실행
  실행문
  ...
```
* 예제
```py
try:
  t1
  print('진행 가능1?')
except Exception as e:
  print(e)

print('진행 가능2?')
```
