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
