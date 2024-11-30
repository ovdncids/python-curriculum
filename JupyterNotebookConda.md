# Jupyter Notebook
## Python 3.8.6, 3.10.12에서 설치
```sh
pip install jupyter
pip install jupyterlab

# 3.8.6인 경우
# ERROR: notebook 7.2.2 has requirement jupyterlab<4.3,>=4.2.0, but you'll have jupyterlab 4.3.1 which is incompatible.
pip install jupyterlab==4.2.3
pip install --upgrade notebook

jupyter --help
## 안되면
source ~/.profile

# notebook.ipynb 파일이 있는 디렉토리로 이동
jupyter notebook
jupyter lab --allow-root --ip=0.0.0.0
## --allow-root = root 사용자로 실행 했을 경우 필요.
## --ip=0.0.0.0 = 외부에서 접속 가능.
```

# Anaconda3 (conda 22.9.0)
## Ubuntu 22.04, Python 3.10.12에서 설치
* https://jongsky.tistory.com/21
