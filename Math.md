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
poetry add scikit-learn
# 사이킷런 라이브러리, 예제 데이터들의 집합
poetry add "scikit-learn<1.8"
```

## 용어
### 실수 (Real number)
* 정수, 분수, 무리수 등을 포함한 모든 숫자

$$
\mathbb{R}
$$

### 묶음 (Tuple)

### 스칼라 (Scalar)
* 실수 하나

### 벡터 (Vector)
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
