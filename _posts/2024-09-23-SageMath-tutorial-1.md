---
title: SageMath 튜토리얼
description: SageMath에 대해 자세히 알아봅시다.
author: 김수진(Sujini)
date: 2024-09-25 02:17:33 +0900
tags: [Tech, Crypto, Tutorial]
categories: [Tech, Crypto, Tutorial]
comments: false
math: true
mermaid: false
pin: false
image: /assets/img/SageMath-tutorial-1/sage-logo.png
---

## 목차

1. SageMath란?
2. SageMath 설치
- Conda를 이용한 Sagemath 설치
3. SageMath 사용하기
- 셸에서 직접 SageMath 사용하기
- Python 스크립트 실행하여 SageMath 사용하기
- SageMath 스크립트 실행하여 SageMath 사용하기
4. SageMath와 Python의 차이점
- 지수 표기법: ** , ^
- 수치형 데이터 타입
- 함수
5. 글을 마치며
6. 참고자료

---
<br>
안녕하세요! Knights of the SPACE의 멤버로 활동하고 있는 김수진(Sujini)입니다.
암호학 분야에서 **SageMath**는 많이 사용되는 툴 중 하나입니다. 이번에는 **SageMath**에 대해 알아보도록 하겠습니다.

---
## SageMath란?
**SageMath**는 다양한 수학 분야를 다루는 컴퓨터 대수 시스템(CAS)으로 **Python** 기반 소프트웨어입니다.

SageMath에 대해 총 2가지 챕터로 구성하여 설명하겠습니다.
1. SageMath 설치 및 Python과의 차이
2. SageMath 기능 

이번 챕터에서는 **SageMath** 설치와 **Python**과의 차이에 관해 설명해 보도록 하겠습니다.

---
## SageMath 설치
Linux나 Windows의 WSL 환경, 그리고 MacOS 환경에서 Conda를 이용한 **SageMath**를 설치하는 과정을 설명하겠습니다.

> [참고] 공식 문서에 따르면 현재 더 이상 Windows용 설치를 지원하지 않으므로, 대신에 WSL(Windows Subsystem for Linux)을 사용하여 Linux 환경에서 **SageMath**를 설치하는 것을 권장하고 있습니다. 
{: .prompt-info}

### Conda를 이용한 Sagemath 설치

먼저 Conda 설치가 필요합니다. Miniforge(또는 Mambaforge), Miniconda 또는 Anaconda 중 하나가 있어야 합니다. 여기서는 Miniforge(또는 Mambaforge)를 설치를 해보도록 하겠습니다.
아래의 명령어를 셸에서 실행하면 됩니다.

```bash
$ curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
$ bash Miniforge3-$(uname)-$(uname -m).sh
```
설치가 완료되면 다음과 같은 메시지와 함께 설치가 완료됩니다.
```bash
...
==> For changes to take effect, close and re-open your current shell. <==

Thank you for installing Miniforge3!
```

아래의 명령어를 입력합니다.<br> 
X는 **Python** 버전을 나타냅니다.`python3 --version`을 이용해 **Python** 버전을 확인할 수 있습니다.
```bash
conda create -n sage sage python=X
```
설치가 완료되면 다음 메시지가 표시됩니다. 설치가 성공적으로 마무리되었습니다.
```bash
...
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate sage
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```
**SageMath** 환경을 활성화하기 위해 `conda activate sage`를 실행한 후, `sage` 명령어를 입력하여 **SageMath** 셸을 열 수 있습니다.
```bash
(base) $ conda activate sage
(sage) $ sage
┌────────────────────────────────────────────────────────────────────┐
│ SageMath version 10.1, Release Date: 2023-08-20                    │
│ Using Python 3.11.9. Type "help()" for help.                       │
└────────────────────────────────────────────────────────────────────┘
sage: 
```

---
## SageMath 사용하기

### 1) 셸에서 직접 SageMath 사용하기
**SageMath**은 **Python**과 같이 셸에서도 직접 사용할 수 있습니다.
```shell
┌────────────────────────────────────────────────────────────────────┐
│ SageMath version 10.1, Release Date: 2023-08-20                    │
│ Using Python 3.11.9. Type "help()" for help.                       │
└────────────────────────────────────────────────────────────────────┘
sage: GF(3)
Finite Field of size 3
sage: GF(3)(1234)
1
```
### 2) Python 스크립트 실행하여 SageMath 사용하기
Conda를 사용하여 **SageMath**를 설치한 경우, **Python** 환경에서도 **SageMath**를 사용할 수 있습니다. 이 경우에는 **Python** 스크립트에 `from sage.all import *`와 같이 **SageMath** 라이브러리를 불러와 사용할 수 있습니다.
```python
from sage.all import *

num = GF(3)(1234)
print(num)
```
**Python**을 실행시키면 다음과 같이 같은 결과값이 나옵니다.
```bash
(sage) $ python3 test.py
1
```
### 3) SageMath 스크립트 실행하여 SageMath 사용하기
**SageMath** 코드를 작성합니다.
```python
num = GF(3)(1234)
print(num)
```
{: file="knights/test.sage" }
그리고 `sage *.sage` 명령어를 입력하여 작성한 **SageMath** 코드를 실행할 수 있습니다. 
```bash
(sage) $ sage test.sage
1
```
> [유의사항] **Python**에 설치된 패키지와 **SageMath**에 설치된 패키지는 개별적입니다.
{: .prompt-warning}

---
## Sage와 Python의 차이점
**Python**의 수학적 기능 때문에 **SageMath**는 여러 면에서 **Python**과 다르게 동작합니다.

**SageMath**는 모든 명령줄을 **Python**으로 전달하기 전에 전처리합니다. 이 과정에서 **SageMath** 고유의 구문과 기능을 **Python** 코드로 변환하여, **Python** 인터프리터가 이를 실행할 수 있도록 합니다. 

예를 들어, 빈 파일 `test.sage`를 생성하고 실행하면 다음과 같은 **Python** 파일이 생성됩니다:
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library




```
{: file="knights/test.sage.py" }
`# This file was *autogenerated* from the file test1.sage`은 이 파일이 자동으로 생성되었음을 나타내는 주석입니다. 그리고 `sage.all_cmdline`을 통해 **SageMath** 라이브러리를 불러옵니다. 

자동으로 생성된 **Python** 파일은 **SageMath** 스크립트에 입력한 명령어를 실행할 수 있도록 준비된 상태입니다.

### 1) 지수 표기법: ** , ^
**Python**에서 `^`는 지수를 의미하지 않고 "xor"을 의미합니다.
`exclusive or` 함수는 거의 사용되지 않기 때문에 이러한 `^`의 사용은 순수 수학 연구에서는 비효율적입니다. 이를 편리하게 사용하기 위해 **SageMath**는 모든 명령 줄을 **Python**으로 전달하기 전에 전처리하여 문자열이 아닌 경우 `**`로 `^`를 대체합니다:

아래의 **SageMath** 스크립트 파일을 실행합니다.
```python
x = 2^3
y = 2^^3
``` 
{: file="knights/test.sage" }
그런 후 생성된 파이썬 파일을 살펴보도록 하겠습니다.
```python

# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_2 = Integer(2); _sage_const_3 = Integer(3)
x = _sage_const_2 **_sage_const_3 
y = _sage_const_2 ^_sage_const_3 


```
{: file="knights/test.sage.py" } 
생성된 **Python** 파일을 보면, 변수 `x`는 **SageMath**에서 사용되는 `^` 연산자가 **Python**의 `**` 연산자로 변환되었습니다. 변수 `y`는 **SageMath**에서 사용되는 `^^` 연산자가 **Python**에서 비트 단위 XOR 연산자인 `^`로 변환되었습니다.

### 2) 수치형 데이터 타입
**Python**과 **SageMath**는 서로 다른 수치형 데이터 타입을 지원합니다. 다음 표는 **Python**과 **SageMath**에서 지원하는 주요 수치형 데이터 타입을 비교한 것입니다:

Python||SageMath
:------:|:---:|:------:
   int/long   |`정수`|sage.rings.integer.Integer
   float   |`실수`|sage.rings.real_mpfr.RealLiteral
   -   |`유리수`|sage.rings.rational.Rational
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; complex &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |`복소수`|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sage.rings.complex_mpfr.ComplexNumber&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

4가지 경우를 각각 자세히 다루어 보도록 하겠습니다.
#### • 정수
**Python의 경우:**
```shell
>>> a = 10
>>> a
10
>>> type(a)
<class 'int'>
```
**SageMath의 경우:**
```shell
sage: a = 10
sage: a
10
sage: type(a)
<class 'sage.rings.integer.Integer'>
```

위와 같이 정수 데이터 타입이 다른 것을 알 수 있습니다.


**SageMath**에 변수 `a`를 정수 `10`으로 할당하는 코드를 작성했습니다.
```python
a = 10
```
{: file="knights/test.sage" }
위 코드를 실행 후 생성된 **Python** 파일을 살펴봅시다.
정수 `10`을 `Integer` 객체로 감싸서 `_sage_const_10`이라는 변수에 할당하고, 이를 다시 변수 `a`에 할당합니다.
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_10 = Integer(10)
a = _sage_const_10 


```
{: file="knights/test.sage.py" }


셸에 `Integer` 객체에 대한 정보를 얻기 위해 `Integer?` 명령을 입력했습니다. 
> **SageMath**에서는 사용자가 함수나 상수의 이름을 입력한 후 물음표를 붙여서 해당 기능에 대한 문서를 쉽게 열람할 수 있습니다.
{: .prompt-tip}
```shell
sage: Integer?
```
내용을 살펴보면 `Integer` 객체는 `GMP` 라이브러리의 `mpz_t` 정수 타입을 래핑(wrapping)합니다. 즉, `Integer` 객체가 정밀도가 높은 정수를 다루며, 내부적으로 `GMP` 라이브러리를 사용한다는 것을 이해할 수 있습니다. 이때, `GMP` 라이브러리는 매우 큰 정수 연산에 최적화된 라이브러리입니다.
```shell
Docstring:     
   The "Integer" class represents arbitrary precision integers. It
   derives from the "Element" class, so integers can be used as ring
   elements anywhere in Sage.

   The constructor of "Integer" interprets strings that begin with
   "0o" as octal numbers, strings that begin with "0x" as hexadecimal
   numbers and strings that begin with "0b" as binary numbers.

   The class "Integer" is implemented in Cython, as a wrapper of the
   GMP "mpz_t" integer type.

...

File:           ~/miniforge3/envs/sage/lib/python3.11/site-packages/sage/rings/integer.pyx
Type:           InheritComparisonMetaclass
Subclasses:     IntegerWrapper

```

#### • 실수
**Python의 경우:**
```shell
>>> a = 10.1234
>>> a
10.1234
>>> type(a)
<class 'float'>
```

**SageMath의 경우:**
```shell
sage: a = 10.1234
sage: a
10.1234000000000
sage: type(a)
<class 'sage.rings.real_mpfr.RealLiteral'>
```
위와 같이 실수 데이터 타입이 다른 것을 알 수 있습니다.


**SageMath**에 변수 `a`를 실수 `10.1234`으로 할당하는 코드를 작성했습니다.
```python
a = 10.1234
```
{: file="knights/test.sage" }
위 코드를 실행 후 생성된 **Python** 파일을 살펴봅시다.
실수 `10.1234`을 `RealNumber` 객체로 감싸서 `_sage_const_10p1234`이라는 변수에 할당하고, 이를 다시 변수 `a`에 할당합니다.
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_10p1234 = RealNumber('10.1234')
a = _sage_const_10p1234 


```
{: file="knights/test.sage.py" }

#### • 유리수
**Python의 경우:**
```shell
>>> a = 2/3
>>> a
0.6666666666666666
>>> type(a)
<class 'float'>
```
**SageMath의 경우:**
```shell
sage: a = 2/3
sage: a
2/3
sage: type(a)
<class 'sage.rings.rational.Rational'>
```
위와 같이 유리수 데이터 타입은 **Python**에는 없고 **SageMath**에 존재한다는 것을 알 수 있습니다.

**SageMath**에 변수 `a`를 유리수 `2/3`으로 할당하는 코드를 작성했습니다.
```python
a = 2/3
```
{: file="knights/test.sage" }
위 코드를 실행 후 생성된 **Pyhton** 파일을 살펴봅시다.
`_sage_const_2`와 `_sage_const_3`는 각각 `Integer(2)`와 `Integer(3)`으로 정의되어 있으며, 이를 통해 `2/3`가 계산됩니다. 유리수 대신 `Integer` 객체를 사용해 연산을 처리하게 됩니다.
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_2 = Integer(2); _sage_const_3 = Integer(3)
a = _sage_const_2 /_sage_const_3 

```
{: file="knights/test.sage.py" }
> 만약 명시적으로 `Rational`을 사용하고 싶다면, 아래와 같이 직접 유리수로 할당하는 코드를 작성할 수 있습니다:
  ```python
  from sage.all import *  
  a = Rational(2, 3)
  ```
{: .prompt-info}

#### • 복소수

**Python의 경우:**
```shell
>>> a = 1 + 2j
>>> a
(1+2j)
>>> type(a)
<class 'complex'>
```
**SageMath의 경우:**
```shell
sage: a = 1 + 2j
sage: a
1.00000000000000 + 2.00000000000000*I
sage: type(a)
<class 'sage.rings.complex_mpfr.ComplexNumber'>
```
위와 같이 복소수 데이터 타입이 다른 것을 알 수 있습니다.

**SageMath**에 변수 `a`를 복소수 `1 + 2j`으로 할당하는 코드를 작성했습니다.
```python
a = 1 + 2j
```
{: file="knights/test.sage" }
위 코드를 실행 후 생성된 **Python** 파일을 살펴봅시다.
정수 `1`을 `Integer` 객체로, 복소수 `2j`를 `ComplexNumber` 객체로 변환한 후, 두 값을 더해 변수 `a`에 `1 + 2j`를 할당한 코드입니다.
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_1 = Integer(1); _sage_const_2j = ComplexNumber(0, '2')
a = _sage_const_1  + _sage_const_2j 


```
{: file="knights/test.sage.py" }

---
#### 간단한 예제
이 예제는 **SageMath**와 **Python** 간의 수치적 데이터 타입 차이가 특정 계산에서 어떻게 다른 결과를 초래하는지를 보여줍니다.

아래의 코드를 **SageMath**와 **Python**에서 실행하면 다른 결과가 나옵니다.
```python
a = (10**309)**(1/3)
```

**SageMath**에서는 정상적으로 실행되지만, **Python**의 경우 아래와 같이 오류 메시지가 뜹니다. 오류 메시지에 의하면 `float`의 최대 범위를 넘어버렸기 때문입니다.
**Python**에서 정수(long)는 메모리가 허용하는 한 무한대로 커질 수 있지만, `float`는 64비트로, 대략 $$1.8 × 10^{308}$$ 까지 표현할 수 있습니다.
```
Traceback (most recent call last):
  File "/Users/gimsujin/Desktop/Knights/test.py", line 1, in <module>
    print((10**309)**(1/3))
          ~~~~~~~~~^^~~~~~
OverflowError: int too large to convert to float
```
좀 더 자세히 셜명을 하면 `10**309`가 먼저 계산되어 정수로 저장되지만, 이어서 `1/3`이 float 타입으로 변환되어 `(10**309)**(1/3)` 계산이 수행될 때 `10**309`를 `float`로 변환하려고 시도하게 됩니다. 이 과정에서 `float`의 최대 범위를 넘어버리게 됩니다.

**SageMath**로 실행 후 생성된 **Python** 파일을 살펴보면, 모든 정수가 `Integer` 객체로 변환되는 것을 알 수 있습니다. 아래의 코드를 통해 해결 방법을 예측할 수 있습니다.
```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_10 = Integer(10); _sage_const_309 = Integer(309); _sage_const_1 = Integer(1); _sage_const_3 = Integer(3)
a = (_sage_const_10 **_sage_const_309 )**(_sage_const_1 /_sage_const_3 )


```
{: file="knights/test.sage.py" }

> [해결 방법] <br>
  `Integer(3)`을 사용하여 `3`을 **SageMath**의 `Integer` 객체로 변환함으로써 해결할 수 있습니다.
  즉, `1/3`이 `float`로 변환되지 않도록 함으로써 문제가 해결될 수 있습니다.
  ```python
  from sage.all import *
  a = (10**309)**(1/Integer(3))
  ```
{: .prompt-tip}

---

### 3) 함수

**SageMath**에서는 기호 변수를 사용하여 함수 정의를 더 간편하게 다룰 수 있는 반면, **Python**에서는 일반적인 함수 정의 방식으로 처리합니다.

**Python의 경우:**
```python
def f(x):
    return x**2 + 3*x + 2
```
{: file="knights/test.py" }

**SageMath의 경우:**
```python
f(x) = x^2 + 3*x + 2 
```
{: file="knights/test.sage" }

```python


# This file was *autogenerated* from the file test.sage
from sage.all_cmdline import *   # import sage library

_sage_const_2 = Integer(2); _sage_const_3 = Integer(3)
__tmp__=var("x"); f = symbolic_expression(x**_sage_const_2  + _sage_const_3 *x + _sage_const_2  ).function(x)


```
{: file="knights/test.sage.py" }

다항식 `x^2 + 3x + 2`를 기호 변수 `x`로 정의하고, 이를 함수로 변환한 것입니다. 이를 통해 나중에 함수 `f`를 호출할 때 `x` 값에 따라 결과를 얻을 수 있습니다.
여기서 `var("x")`는 **SageMath**에서 변수를 기호로 취급하게 만듭니다. 이는 함수나 수식을 상징적으로 다루기 위한 중요한 작업입니다.

---
### 글을 마치며
이번 글은 SageMath의 설치 방법과 기본 사용법, 그리고 Python과의 차이점을 다루었습니다. 다음 글에서는 SageMath의 실제로 쓰는 기능을 다뤄보겠습니다. 읽어주셔서 감사합니다!

---
### 참고자료
- https://www.sagemath.org