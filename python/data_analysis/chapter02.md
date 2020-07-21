# CHAPTER 2. 파이썬 프로그래밍
[실습 내용](https://github.com/rladnswl30/python-data-analysis)
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

## IDE
https://www.programiz.com/python-programming/ide  
Visual Studo Code VS Intellij  
Intellij가 익숙해서.. Intelij에 venv 설정하여 진행중...

## 2.3.2 파이썬 연산자 우선순위
|연산자|설명|
|---|---|
|() | 그루핑|
|f(args..) | 함수 호출|
|x[index:index]| 슬라이싱|
|x[index]|인덱싱|
|x.속성|속성 참조|
|**|거듭제곱|
|~x|비트연산 NOT|
|+x, -x|양, 음|
|*, /, %|곱셈, 나눗셈, 나머지|
|+, -|덧셈, 뺄셈|
|<<, >> | 비트 이동|
|&|비트 연산 AND|
|^|비트 연산 XOR|
| \| | 비트 연산 OR|
|in, not in, is, is not, <, <=, >, >=, <>, !=, ==| 비교|
|not x | 논리 연산 NOT|
|and | 논리 연산 AND|
|or| 논리 연산 OR|
|lambda| 람다 표현식|

우선 순위에서 가장 높은 괄호만이라도 기억하자. 우선순위를 잘 모르면 무조건 괄호쓰기!

## 2.4.2 변경이 불가능한 튜플 ([참고](https://wikidocs.net/15))
- 튜플은 리스트처럼 다양한 자료형의 원소를 가진다.
- 대괄호 대신 소괄호로 표시하며, 원소를 변경할 수 없다.

## 2.4.3 {키:값} 형태 딕셔너리
- 키와 값을 하나의 원소로 가지는 순서가 없는 집합  
- 키:값 형태의 원소드를 쉼표로 구분하여 중괄호로 감싸서 표시한다.  
- 순서가 없어서 인덱스로 값에 접근하는 것 불가  

## 2.4.5 중복 없는 셋
```python
s = {'A', 'P', 'P', 'L', 'E'}
```
- Set은 다른 자료형보다 검색 시간이 훨씬 빠르다.
- Set은 중괄호 사이에 원소들을 쉼표로 구분하여 나열한다.  
- 중복을 허용하지 않아 원소를 중복해서 생성해도 중복을 제거하여 하나만 존재하게 된다.  
- 순서는 보장하지 않는다. 위 순서대로 생성해도 실제 print 해보면 순서가 다를 수 있음.
- 인덱싱이 불가하다.
- 교집합, 합집합, 차집합은 구할 수 있다.

## 2.4.6 타임잇으로 성능 측정하기
timeit 측정 결과...   
원소를 단순히 순회하는 것이 아닌,   
방대한 원소 중에 특정 원소가 존재하는지 검색할 때에는 set이 빠르다.

## 2.5.1 변수
- python은 다른 프로그래밍 언어와 달리 정수형(int) 크기에 제한이 없어서 10의 100승도 처리 가능
- dir()함수 : 해당 객체가 갖고 있는 함수와 변수 리스트 확인 가능
- 예약어 : 파이썬에서 이미 사용하고 있는 용도가 예약된 단어들. 문법적 용도로 사용

## 2.5.2 함수
- None 반환값 : 함수 정의 시 반환값을 지정하지 않으면 None을 반환
- |함수|procedure|method
  |--|--|--|
  |결과값을 반환<br>클래스에 속하지 않는 함수|결과값을 반환하지 않는 것|클래스에 속하는 함수
- 람다
```
def lambda (인수) :
  return 표현식
```
- [내장 함수 리스트](https://github.com/INVESTAR/StockAnalysisInPython/blob/master/10_Appendix_(Python_Built-in_Functions_and_AES-256_Encryption).pdf)

## 2.6.1 모듈
#### 모듈 ?  
.py 확장자를 갖는 파일 모두를 뜻한다.  
여러 .py 모듈들을 특정 디렉토리에 모아놓은 것을 패키지라고 부른다.  
이러한 모듈 또는 패키지를 가리켜 라이브러리 라고 부른다.

- module.kwlist : 모듈의 예약어 확인
- module.\_\_file\_\_ : 모듈의 실제 위치 확인
- from ~ import   : module or package명 생략 가능
```
from module import class or function
from package import module
```
- import ~ as ~ : 별칭 사용 가능
```
import 이름이_긴_모듈명 as 별칭
from ~ import ~ as 별칭
```

## 2.6.2 패키지
- 패키지의 경로 속성 : package.\_\_path\_\_ 가 존재하면 패키지
- import 하면 import한 모듈의 디렉토리에는 \_\_pycache\_\_ 디렉터리가 생기고, 그 안에는 .pyc파일이 생성된다. (캐시)
- \_\_init\_\_.py : 해당 디렉토리를 패키지로 인식  
python 3.3 이상에서는 없어도 된다.

### 2.7.2 상속
```
class 자식 클래스(부모 클래스 1, 부모 클래스 2, ...):
  pass
```

### 2.7.4 클래스 메서드
- \_\_init\_\_ 생성자 : 클래스 인스턴스가 생성될 때 자동으로 호출되는 메서드  
- \_\_del\_\_ 소멸자 : 인스턴스가 메모리에서 제거될 때 자동으로 호출되는 함수  
가비지 컬렉터에 의해 자동적으로 메모리에서 제거  
명시적으로 호출하여 메모리에서 인스턴스 제거 가능
- """설명""" 을 적은 후 help(클래스) 호출하면 설명을 포함하여 doc string을 출력한다.

