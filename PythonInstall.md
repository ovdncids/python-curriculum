# Python 설치

## Pyenv (Node.js의 NVM과 비슷함)
* 여러 버전의 Python을 설치 할 수 있다.

### Mac
* ❕ `Mac`은 `system`의 `Python3`에 직접 `pip3 install pipenv`와 같이 `system 패키지` 설치를 막는다. (운영체제 동작 및 보안에 문제 때문에)
* https://github.com/pyenv/pyenv
* http://taewan.kim/post/python_virtual_env
```sh
# pyenv 설치
brew install pyenv

# 우선 설치 사항
sudo xcode-select --install
brew install zlib
brew install xz
# python 설치
pyenv install 3.7.4

# 설치된 버전들 보기
pyenv versions
# 글로벌 버전 변경
pyenv global 3.7.4
# 해당 경로 마다 버전 변경 (`.python-version` 파일이 생성, 수정)
pyenv local 3.7.4
# 버전 변경 (버전만 변경되고 `.python-version` 파일은 수정 하지 않음)
pyenv shell 3.7.4
# 버전 해제
pyenv local --unset
  # 해당 프로젝트에서 `.python-version` 파일이 삭제 된다.

# 1회성 Python 버전 선택
eval "$(pyenv init -)"
# pyenv 설정 zsh셸
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
# pyenv 설정 bash셸
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
  # .bashrc는 bash명령을 실행 하면 실행 된다
# or
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
  # .bash_profile는 새로운 셸을 실행 하면 실행 된다

pip list
  # pip install로 설치되어 있는 라이브러리를 볼 수 있다.
```
* <details><summary>M1 - <code>brew install zlib</code> 설치 안 될때</summary>

  ```sh
  vi ~/.zshrc

  # Python zlib
  export LDFLAGS="-L/opt/homebrew/opt/zlib/lib -L/opt/homebrew/opt/bzip2/lib -L/opt/homebrew/opt/ncurses/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/zlib/include -I/opt/homebrew/opt/bzip2/include -I/opt/homebrew/opt/ncurses/include"
  export PKG_CONFIG_PATH="/opt/homebrew/opt/zlib/lib/pkgconfig:/opt/homebrew/opt/bzip2/lib/pkgconfig:/opt/homebrew/opt/ncurses/lib/pkgconfig"

  source ~/.zshrc
  brew install zlib
  ```
</details>

<!--
#### Mac Big Sur
* https://github.com/pyenv/pyenv/issues/1643
```sh
pyenv install --patch 3.7.4 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch)
```
-->

### 윈도우
* https://github.com/pyenv-win/pyenv-win
* https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#pyenv-win-zip
```sh
다운로드 pyenv-win
C:\Users\사용자\.pyenv 폴더에 풀기
환경 변수 > 시스템 변수 > Path > 
  C:\Users\사용자\.pyenv\pyenv-win\bin

# 사용자 변수에 추가
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_ROOT',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
# 사용자 변수 path에 추가
[System.Environment]::SetEnvironmentVariable('path', $env:USERPROFILE + "\.pyenv\pyenv-win\bin;" + $env:USERPROFILE + "\.pyenv\pyenv-win\shims;" + [System.Environment]::GetEnvironmentVariable('path', "User"),"User")
# 변수가 잘 추가 되었는지 확인
pyenv --version
# home directory에서 pyenv설정
pyenv rehash

# python 설치
pyenv install 3.7.4
pyenv versions
# 글로벌 버전 변경
pyenv global 3.7.4
# 해당 경로 마다 버전 변경
pyenv local 3.7.4
  # 하지만 cmd가 열리고 처음 python 또는 pyenv가 실행 된 경로의 버전으로 cmd 끝날때 까지 적용 된다
# 버전 선택
pyenv shell 3.7.4
```

## Pipenv (node_modules와 비슷함)
* 가상환경으로 해당 경로를 선택, 종료 할 수 있다.
* 가상환경만의 패키지를 설치 한다.
```sh
pip install pipenv
  # Pipenv 설치
```
```sh
pipenv --python 3.8.3
  # ❕ `pyenv versions`에 있는 버전을 선택 한다. 선택하지 않으면 `system` 버전이 선택될 수 있다.
pipenv --python "C:\Users\Administrator\.pyenv\pyenv-win\versions\3.9.4\python.exe"
  # 강제로 해당 경로의 버전을 선택한다.
pipenv shell
  # 해당 경로를 가상환경으로 선택한다.
  # 새로운 shell이 시작 된다. (`pip list`의 라이브러리도 초기화되어 시작된다.)
pipenv --venv
  # 현재의 가상 경로를 볼 수 있다.
pipenv --rm
  # pipenv 환경 설정을 지운다.
  # 잘 안지워지면 해당 설정 파일을 직접 지운다.
pipenv install django
  # 패키지 설치
pipenv graph
  # 설치된 패키지를 볼 수 있다. (pip freeze)
deactivate
  # 가상환경 종료
  # 가상환경 설정을 해제 하려면 해당 프로젝트에서 (Pipfile, Pipfile.lock) 파일 삭제
```

### Windows에서 Pipenv shell 이후 `up/down arrow`으로 명령 히스트로가 동작 하지 않을때
https://github.com/pypa/pipenv/issues/876
```sh
python -m pipenv shell
```
