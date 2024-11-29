# Jupyter Notebook

## Python 3.8.6에서 설치
```sh
pip install jupyter

# ERROR: notebook 7.2.2 has requirement jupyterlab<4.3,>=4.2.0, but you'll have jupyterlab 4.3.1 which is incompatible.
pip install jupyterlab==4.2.3
pip install --upgrade notebook
pip install jupyter

jupyter --help
## 안되면
source ~/.profile

# notebook.ipynb 파일이 있는 디렉토리로 이동
jupyter lab
```
