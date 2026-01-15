# Python 설치
* `3.10.18` 가장 안정적, `3.11.13` 새로운 프로젝트, `3.12.11` 이상은 아직 안정적이지 않음, 이전은 유지보수

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
pyenv install 3.10.18

# 설치된 버전들 보기
pyenv versions
# 글로벌 버전 변경
pyenv global 3.10.18
# 해당 경로 마다 버전 변경 (`.python-version` 파일이 생성, 수정)
pyenv local 3.10.18
# 버전 변경 (버전만 변경되고 `.python-version` 파일은 수정 하지 않음)
pyenv shell 3.10.18
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

<!--
#### Mac Big Sur
* https://github.com/pyenv/pyenv/issues/1643
```sh
pyenv install --patch 3.7.4 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch)
```
-->

### 윈도우
* `윈도우`는 `Mac`보다 낮은 버전 설치를 지원하고, 높은 버전은 `Python 소스`를 빌드해서 설치해야 한다.
* https://github.com/pyenv-win/pyenv-win
* https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#pyenv-win-zip
```sh
다운로드 pyenv-win
C:\Users\사용자\.pyenv 폴더에 풀기
환경 변수 > 시스템 변수 > Path > 
  C:\Users\사용자\.pyenv\pyenv-win\bin

# 사용자 변수에 추가 (PowerShell)
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_ROOT',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
# 사용자 변수 path에 추가
[System.Environment]::SetEnvironmentVariable('path', $env:USERPROFILE + "\.pyenv\pyenv-win\bin;" + $env:USERPROFILE + "\.pyenv\pyenv-win\shims;" + [System.Environment]::GetEnvironmentVariable('path', "User"),"User")
# 변수가 잘 추가 되었는지 확인
pyenv --version
# home directory에서 pyenv설정
pyenv rehash

# python 설치 가능한 버전 확인
pyenv install --list
# python 설치
pyenv install 3.10.11
pyenv versions
# 글로벌 버전 변경
pyenv global 3.10.11
# 해당 경로 마다 버전 변경
pyenv local 3.10.11
  # 하지만 cmd가 열리고 처음 python 또는 pyenv가 실행 된 경로의 버전으로 cmd 끝날때 까지 적용 된다
# 버전 선택
pyenv shell 3.10.11
```

#### PowerShell 오류
```ps1
# 보안 정책 수정 (둘중 하나는 됨)
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

# 현재 세션의 보안 정색 보기
Get-ExecutionPolicy -List
```

## Poetry (NPM과 Yarn이 섞인 느낌)
* https://python-poetry.org/docs/#installing-with-the-official-installer

### Windows
```sh
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -
```
* 설치후 `PATH` 관련 문구 확인. (`PATH` 추가 후 VSCode 재시작)

```sh
# 명령어 리스트
poetry list
# 새로운 프로젝트
poetry new poetry-study
# 이미 존재하는 프로젝트
poetry init
# 가상 환경 정보
poetry env info
# 기존 프로젝트 설치 (pyproject.toml 락파일을 바탕으로 가상환경에 라이브러리를 설치함, npm install과 비슷함)
poetry install
# 가상 환경 들어가기(확인용, 잘 안씀)
poetry shell
# 가상 환경 나가기
deactivate
# 라이브러리 설치
poetry add numpy
# 개발용으로 라이브러리 설치
poetry add --group dev ipython
# 현재 가상환경에 설치된 라이브러리 보기
poetry show
# IPython 실행
poetry run ipython ./tests/__init__.py
```

* <details><summary>Pipenv (이제 사용하지 않음)</summary>

  ## Pipenv (node_modules와 비슷함)
  * 가상환경으로 해당 경로를 선택, 종료 할 수 있다.
  * 가상환경만의 패키지를 설치 한다.
  ```sh
  pip install pipenv
    # Pipenv 설치
  ```
  ```sh
  pipenv --python 3.11.13
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
    # 잘 안지워지면 `가상환경 경로`와 `Pipfile` 파일을 직접 지운다.
  pipenv install django
    # 패키지 설치
  pipenv graph
    # 설치된 패키지를 볼 수 있다. (pip freeze)
  deactivate 또는 exit
    # 가상환경 종료
    # 가상환경 설정을 해제 하려면 해당 프로젝트에서 (Pipfile, Pipfile.lock) 파일 삭제
  ```
  
  ### Windows에서 Pipenv shell 이후 `up/down arrow`으로 명령 히스트로가 동작 하지 않을때
  https://github.com/pypa/pipenv/issues/876
  ```sh
  python -m pipenv shell
  ```
  
  ### VSCode > Run and Debug > pipenv --venv 경로가 다른곳으로 실행 되는 경우
  .vscode/settings.json
  ```sh
  {
      "python.defaultInterpreterPath": "{pipenv --venv 경로}\\Scripts\\python.exe"
  }
  ```
</details>
