# PyTorch (2.7.1+cu118)

## 설치
* CPU
```sh
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

* GPU
```sh
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

## 기본 사용법
hello.py
```py
import torch
print(torch.__version__)
print(torch.cuda.is_available())
```
