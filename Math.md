# 수학식 (Math expression)
* https://datascienceschool.net/02%20mathematics/00.00%20%EC%86%8C%EA%B0%9C%EC%9D%98%20%EA%B8%80.html

## 그리스 문자 (Greek letters)
### 조판 언어 (LaTeX commands)
#### 인라인 수식 (Inline math)
* `$ \alpha = \beta $`

$$
\alpha = \beta
$$

#### 디스플레이 수식 (Display math)
* `$$ \gamma $$`

$$
\gamma
$$

## 수열 (Sequnce)
* 컴퓨터의 배열과 유사하지만 index가 1부터 시작하고 순서가 중요 하며 주로 무한을 표현 한다.

$$
x_1, x_2, \ldots, x_N
$$

### 수열의 합 (sum, 시그마)
* i가 1부터 N까지 합

$$
\sum_{i=1}^{N} x_i = x_1 + x_2 + \ldots + x_N
$$

* i가 1부터 9까지의 10i의 합

$$
\sum_{i=1}^{9} 10i = 10·1 + 20·2 + \ldots + 10·9
$$

### 수열의 곱 (Product, 파이)
* 원주율 파이는 `\pi`
* i가 1부터 N까지의 곱

$$
\prod_{i=1}^{N} x_i = x_1 · x_2 · \ldots · x_N
$$

## 집합 (Set), 원소 (Element)
* 순서가 중요하지 않은 숫자들의 집합

$$
\\{ x_1, x_2 \\}
$$

# 난수
```py
np.random.randint(10, size=10)
```

# 선형 대수 (Linear Algebra)
```sh
# Python@3.10.11, Poetry@2.2.1
poetry add "numpy<2.0"
poetry add matplotlib
poetry add imageio
poetry add "scikit-learn<1.8"  # 사이킷런 라이브러리, 예제 데이터들의 집합

import math
import numpy as np
import matplotlib.pylab as plt
import imageio.v2 as imageio
from sklearn.datasets import load_iris
```

## 용어
### 실수 (Real number)
* 정수, 분수, 무리수 등을 포함한 모든 숫자

$$
\mathbb{R}
$$

### 묶음 (Tuple)

### 단일값, 스칼라 (Scalar)
* 실수 하나

### 방향값, 벡터 (Vector)
* 스칼라의 집합. 1차 배열
* `{1980, 1210, 169, 46}` 이는 `4차원(4-dimensinal) 벡터`이고 순서가 중요 하다.
```py
np.array([1980, 1210, 169, 46])
```

### 행렬 (Matrix, Column Vector)
* 동일한 벡터의 집합. 2차 배열
```py
np.array([
  [1980, 1210, 169, 46],
  [1995, 1113, 152, 31]
])
```

### 텐서 (Tensor)
* 동일한 행렬의 집합. 3차 배열

### 전치 연산 (Transpose)
* 행과 열을 바꾸는 연산.
* 전치 연산으로 만든 행렬을 전치행렬이라 한다.
* 이미지를 왼쪽으로 90도 돌린다고 생각하면 쉽다. `np.rot90(t, 1)`
```py
t = np.array([
  [1980, 1210, 169, 46],
  [1995, 1113, 152, 31]
])
t.T
# [[1980, 1995],
# [1210, 1113],
# [ 169,  152],
# [  46,   31]]

# T를 2번 쓰면 원복된다.
(t.T).T
```

### 배열 확장, 브로드캐스팅 (Broadcasting)
```py
np.array([1, 2, 3]) + 1
# [2, 3, 4]
```

### 내적 (Inner Product, Dot Product)
* 같은 위치에 있는 성분끼리 곱해 모두 더한것
```py
i1 = np.array([1, 2, 3])
i2 = np.array([4, 5, 6])
np.dot(i1, i2)
# 또는
i1 @ i2
# 1 * 4 + 2 * 5 + 3 * 6 = 32

# 평균 구하기
d1 = np.arange(10)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
length = len(x)
d2 = np.ones(length)
# [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
d2 @ x / length
# 4.5
d1.mean()
# 4.5
```

### 사인 (Sin), 코사인 (Cos[Co-: 보충]), 탄젠트 (기울기: Tangent)
* θ: 각도, 세타 (Theta)
* 직각삼각형의 높이: 𝑎 = 6, 밑변: 𝑏 = 8, 빗변: h = 10
* sin(θ): 빗변 대비 높이 비율: 6 / 10 = 0.6
* cos(θ): 빗변 대비 밑변 비율: 8 / 10 = 0.8
* tan(θ): 밑변 대비 높이 비율: 6 / 8 = 0.75
```py
a = 6  # 높이
b = 8  # 밑변
h = 10  # 빗변
sin_theta = a / h
cos_theta = b / h
tan_theta = a / b
sin_theta_deg = math.degrees(math.asin(sin_theta))
cos_theta_deg = math.degrees(math.acos(cos_theta))
tan_theta_deg = math.degrees(math.atan(tan_theta))
print("sin(θ) =", sin_theta)  # 0.6
print("cos(θ) =", cos_theta)  # 0.8
print("tan(θ) =", tan_theta)  # 0.75
print("sin으로 θ를 구하면: ", sin_theta_deg, "도")  # 36.86989764584402
print("cos으로 θ를 구하면: ", cos_theta_deg, "도")  # 36.86989764584401
print("tan으로 θ를 구하면: ", tan_theta_deg, "도")  # 36.86989764584402
```
```py
theta = math.radians(336.86989764584402)
print(math.tan(theta))  # 0.75
```

### 유사도 (Similarity)
* 두 벡터의 닮은 정도를 정량적으로 나타낸 값
