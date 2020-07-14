# CHAPTER 2. 파이썬 프로그래밍
## 파이썬 특징
- 간결한 코드
- 풍부한 표준 라이브러리
- 직관적인 문법

## 파이썬 3.X 버전 설치
- 하위 호환을 지원하지 않는다. (상위 버전 설치를 유도)
- 3.x 버전에서 표준 라이브러리가 재배치 되었을 뿐 아니라 문자열을 유니코드로 처리해서 한글 처리가 훨씬 쉽다.

homebrew 혹은 https://www.python.org/downloads/  
설치 후, python3 -V 버전 확인

## python3를 default로 실행하기 python3
```
brew install python3

python3 --version

vi ~/.bash_profile 에 추가
alias python=/usr/local/bin/python3.8
alias pip=/usr/local/bin/pip3

source ~/.bash_profile
```

## pip을 이용한 패키지 설치
PyPI(Python Package Index)에서 21만개가 넘는 파이썬 package를 관리한다.  
```
pip install {packageName} : package install
pip list : 모든 package list
pip freeze : pip로 직접 설치한 package list
```
책에서 사용하는 package : https://github.com/INVESTAR/StockAnalysisInPython/blob/master/02_Python_Programming/requirements.txt
```
pip install -r requirements.txt
```

## 32bit python 가상화(venv) 설치
국내 증권사에서 제공하는 COM(Component Object Model)방식의 시스템 트레이딩 API를 사용하려면 32비트 python을 설치해야한다.
> https://www.python.org/downloads/windows/  
Windows x86 executable installer
```
mkdir pythonVirtual
cd pythonVirtual
python -m venv Py380_32
notepad Py380_32\pyvenv.cfg
32bit python 경로 및 버전 지정
Py380_32\Scripts\active 가상환경 활성화
```

### IDE
https://www.programiz.com/python-programming/ide  
Visual Studo Code VS Intellij  
Intellij가 익숙해서.. Intelij에 venv 설정하여 진행중...