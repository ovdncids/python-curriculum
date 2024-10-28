# GME_tutorials - Python 3.11.9
* https://github.com/xuhuihuang/GME_tutorials/tree/main

## msmbuilder2022
* https://github.com/msmbuilder/msmbuilder2022
```sh
pip install git+https://github.com/msmbuilder/msmbuilder2022.git
```

### distutils.errors.DistutilsPlatformError: Microsoft Visual C++ 14.0 or greater is required
* https://integer-ji.tistory.com/368
```sh
https://visualstudio.microsoft.com/ko/visual-cpp-build-tools
Build Tools 다운로드
C++를 사용한 데스크톱 개발만 체크
설치 후 재부팅
```

## python 3.12 관련 오류
### fastcluster
* Windows `python 3.12` 버전은 `msmbuilder2022` 설치 시 `fastcluster` 오류 발생 한다.

### pip install numpy==1.23.5
* `python 3.12` 버전은 내장된 `numpy` 라이브러리가 1.23.5 보다 높아서, `villin_headpiece_tutorial.ipynb` 파일 `igme.top_outputs` 함수에서 `numpy` 관련 오류가 발생한다.
