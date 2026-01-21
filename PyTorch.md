# PyTorch (2.7.1+cu118)

## 설치
* CPU
```sh
# pip
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu

# Poetry
poetry source add pytorch https://download.pytorch.org/whl/cpu --priority supplemental
poetry add torch torchvision torchaudio --source pytorch
```

* GPU (M1 안됨)
```sh
# pip
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Poetry
poetry source add pytorch https://download.pytorch.org/whl/cu118 --priority supplemental
poetry add torch torchvision torchaudio --source pytorch
```

## 기본 사용법
hello.py
```py
import torch
print(torch.__version__)
print(torch.cuda.is_available())
```
