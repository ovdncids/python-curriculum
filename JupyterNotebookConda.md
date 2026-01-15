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

## Python 3.10.11, Poetry@2.2.1, JupyterLab@4.5.2
```sh
poetry init
poetry add --group dev jupyterlab
poetry run jupyter lab
```

# Anaconda3 (conda 22.9.0)
## Ubuntu 18.04, 20.04, 22.04
* https://jongsky.tistory.com/21
* `Anaconda3`는 `python 가상환경`을 제공하므로 `python`을 미리 설치 할 필요 없다.
```sh
apt update
curl --output anaconda.sh https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
# 정상적인 파일인지 확인
sha256sum anaconda.sh
bash anaconda.sh
echo "# Anaconda3 (conda 22.9.0)" >> ~/.bashrc
echo "export PATH=~/anaconda3/bin:~/anaconda3/condabin:$PATH" >> ~/.bashrc
source ~/.bashrc
conda --version
# conda 가상환경 생성
conda create -n python3.10.12 python=3.10.12
# conda 가상환경 사용
conda activate python3.10.12
# conda 가상환경 종료
conda deactivate
# conda 가상환경 리스트
conda info --envs
# conda 가상환경 삭제
conda remove --name python3.10.12 --all
```

### M1에서 /lib64/ld-linux-x86-64.so.2 오류 발생시
* https://stackoverflow.com/questions/68630526/lib64-ld-linux-x86-64-so-2-no-such-file-or-directory-error
```sh
docker run --platform linux/x86_64 -it --name ubuntu-22.04 -p 8888:8888 ubuntu:22.04
## --platform linux/x86_64 = AMD64용 ubuntu:22.04을 설치한다.
```

## Anaconda3 (conda 24.9.2) - Docker Image
* [continuumio/anaconda3](https://hub.docker.com/r/continuumio/anaconda3?uuid=5e4011a2-db0d-4643-a964-29e2cc16147b%0A)
* [continuumio/miniconda3](https://hub.docker.com/r/continuumio/miniconda3?uuid=5e4011a2-db0d-4643-a964-29e2cc16147b%0A)
```sh
# Anaconda3 (3.69 GB)
docker run -it --name anaconda3 -p 8888:8888 continuumio/anaconda3
# Miniconda3 (554.47 MB)
docker run -it --name miniconda3 -p 8888:8888 continuumio/miniconda3
```
* `Python 3.12.7` 가상환경이 설치되어 있다.
