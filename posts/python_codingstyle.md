<!--
.. title: 파이썬 코딩 스타일
.. slug: python_codingstyle
.. date: 2012-10-09 17:34:27 UTC+09:00
.. tags: Python
.. category: python
.. link: 
.. description: 파이썬 코드를 작성할때 참고할것
.. type: text
-->

출처: *박응용,'Jump to Python',p439~440,2001,정보 게이트*

코딩이란 프로그램을 작성하는 행위, 좋은 스타일이라고 알려져 있는 몇 가지 방법이 존재한다. 그것들에 대해서 살펴보자.

# 이름결정 : 
함수나 변수들의 이름을 지을 때 생각할점.

## 변수명을 구체적으로 하자
```python 
a=[1,2,3]
number=[1,2,3]
```
   
> 발음하기 쉽게 이름을 짓자
  
## 함수의 입력값을 받는 변수 앞에는 the를 붙이자
```python
def writediary(theMonth,theDay):
    nexDay= theDay+1
```

## 참과 거짓을 나타내는 변수에는 is를 붙이자

```python
isProgrammer = 1
isStudent = 0
```

## 상황에 따라 변수명을 결정하자
보통 순환문에 사용되는 변수에는 i,j,k 등이 관례적으로 사용됨
```python
i = 0
while 1:
    i = i+1
```

## 함수는 '동사+명사'식으로 짓자
```python
def makehouse(theTree,theCement):
    pass
```

## 함수에 들어오는 입력 값이 너무 많으면 딕셔너리로 대치하자
```python
def makehouse(theTree,theCement,the.......):
    pass
```
보다는

```python
def makehouse(theManyinput):
        theTree = theManyinput['tree']
        theCement = theManyinput['cement']
```

## 클래스 이름은 대문자로

```python
class Person:
    pass
```

## 주석활용
자신이 작성한 코드의 의도를 알려주고 싶을 때 주석을 사용하자. 구체적으로 달고 가능하면 영어로 달자.

```python
# FIXME: 코드를 고쳐야 할 부분을 나타냄
# TODO: 앞으로 어떻게 코드를 수정하고 싶은지에 대한 내용
# XXX: 뭔가 잘못이 있는 것 같은 부분
```

# 마무리하며,
보기 좋은 코드가 읽기도 좋고 분석하기도 좋다. 다만 지키기 쉽지 않다는것!