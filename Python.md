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
