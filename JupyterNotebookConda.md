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
jupyter lab --allow-root --ip=0.0.0.0 --port=8888
## --allow-root = root 사용자로 실행 했을 경우 필요.
## --ip=0.0.0.0 = 외부에서 접속 가능.
```

# Anaconda3 (conda 22.9.0)
## Ubuntu 22.04, Python 3.10.12에서 설치
* https://jongsky.tistory.com/21
```sh
curl --output anaconda.sh https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
# 정상적인 파일인지 확인
sha256sum anaconda.sh
bash anaconda.sh
sudo vi ~/.bashrc
# Anaconda3 (conda 22.9.0)
export PATH=~/anaconda3/bin:~/anaconda3/condabin:$PATH
source ~/.bashrc
conda --version
# conda 가상 환경 생성
conda create -n python3.10.12 python=3.10.12
# conda 가상 환경 사용
conda activate python3.10.12
```

### M1에서 /lib64/ld-linux-x86-64.so.2 오류 발생시
* https://stackoverflow.com/questions/68630526/lib64-ld-linux-x86-64-so-2-no-such-file-or-directory-error
```sh
docker run --platform linux/x86_64 -it --name ubuntu-22.04 -p 8888:8888 ubuntu:22.04
## --platform linux/x86_64 = AMD64용 ubuntu:22.04을 설치한다.
```
