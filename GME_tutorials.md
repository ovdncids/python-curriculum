# GME_tutorials
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

### fastcluster 오류
* `python 3.11` 버전으로 `msmbuilder2022` 설치

## alanine_dipeptide_tutorial.ipynb
### pip install numpy==1.23.5
* python 3.12 버전은 `numpy`가 이미 설치되어 있다.
```diff
- pip install numpy==1.23.5
+ pip install numpy
```
