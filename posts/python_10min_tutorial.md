<!--
.. title: 10분안에 배우는 파이썬
.. slug: python_10min_tutorial
.. date: 2015-06-16 16:25:18 UTC+09:00
.. tags: Python
.. category: python
.. link: 
.. description: 파이썬 10분안에 배우기, 진짜로? 
.. type: text
-->

> 파이썬 2.7 버전 기준입니다.

Python을 배우고 싶고, 간략하면서도 내용이 알찬 튜토리얼을 찾고 있는가? 이 튜토리얼은 Python 을 10분 만에 가르쳐줄 것이다. 기본 개념들을 설명해서, 여러분이 파이썬 프로그래밍을 시작할 수 있게 도와줄 것이다. 물론 제대로 배우려면, 실제로 파이썬으로 프로그래밍을 꽤 해봐야 할 것이다. 여러분이 이미 다른 프로그래밍 언어를 사용해 본적이 있다고 생각하고, 아주 기본적인 내용들은 다루지 않고, 파이썬의 특징들을 주로 다룰 것이다. 주의 깊게 보기 바란다.

# Properties

파이썬은 strongly-typed (역주: 즉 타입을 확인한다, 인터프리터가 타입을 알고 있다), dynamically-typed (역주: 변수의 타입을 실시간으로 변경할 수 있다, 변수자체가 타입을 갖는 것이 아니라 변수의 값이 타입을 갖는다), implicitly typed (변수에 타입을 정해서 선언하지 않는다. String myString = "a" 가 아닌, my_string = "a" 이라고 선언한다) 타입을 갖는다.
또한, case sensitive (Var 와 var 는 다른 변수이다) 하고, 객체 지향적 (모든것이 객체이다) 이다.

# 도움 얻기

인터프리터에서 도움을 받을 수 있다. 어떤 객체에 대해 알고 싶으면, 인터프리터에서 help() 와 dir() 을 이용한다, dir() 은 객체의 속성,메써드들을 보여준다. 그리고 .__doc__ 으로 객체의 문서를 볼 수 있다:

```python
help(5) # int 객체의 help 메시지를 보여준다: (etc etc)
dir(5) # 객체의 속성, 메써드들을 보여준다
```
    ['__abs__', '__add__', ...]

```python
abs.__doc__
```
    'abs(number) -> number
    인자의 절대값을 리턴한다.'

# 문법(Syntax)

파이썬은 코드의 끝을 ** ; ** 등으로 특별히 표시하지 않는다. block 은 줄맞춤 (indentation) 으로 표현한다. block 을 사용하는 문장 (if, else 등) 은 : 을 끝에 붙인다. 한줄짜리 주석은 # 을 사용하고, 여러줄에 걸친 주석은 """ 주석 """ 을 사용한다. 객체에 값을 할당할 때에는 = 을 사용하고, 두 객체를 비교할 때에는 == 을 사용한다. += 와 -= 으로 값을 증가/감소할 수 있다.

```python
myvar = 3
myvar += 2
myvar
```
    5

```python
myvar -= 1
myvar
```
    4

```python
"""여러줄짜리 주석이다.
어쩌고 저쩌고..."""
mystring = "Hello"
mystring += " world."
print mystring
```
    Hello world.

변수 두개를 서로 바꿔준다!

```python
myvar, mystring = mystring, myvar
```

# 데이터형(Data types)

파이썬은 리스트, tuple (튜플), dictionary, set 데이터 타입을 제공한다. list 는 여러개의 원소를 가지고, 다른 리스트를 원소로 가질 수도 있다. dictionary 는 연관배열 (associative array, hash table 로 key/value 를 저장함) 이고, tuple 은 변경이 불가능한 배열이다. 이들 컨테이너에 여러개 타입의 객체들을 섞어서 넣을 수 있다. list 나 tuple 등의 배열 형식의 컨테이너에서 첫번재 인자의 인덱스는 0 이다. -1 은 배열의 마지막 원소의 인덱스이며, -2 는 마지막에서 두번째 인덱스이다. 그리고 파이썬에서는, 변수에 함수를 지정할 수 있다.

```python
sample = [1, ["another", "list"], ("a", "tuple")]
mylist = ["List item 1", 2, 3.14]
mylist[0] = "List item 1 again" # 첫번째 원소를 변경한다
mylist[-1] = 3.21 # 마지막 원소를 변경한다.
mydict = {"Key 1": "Value 1", 2: 3, "pi": 3.14}
mydict["pi"] = 3.15 # dictionary 값을 변경한다
mytuple = (1, 2, 3)
myfunction = len # myfunction 변수가 len 이라는 함수를 가리키도록 한다
print myfunction(mylist)
```
    3

`:` 을 이용하여 배열의 구간을 표현한다. `:` 을 사용할 때 앞의 index 가 없으면 0 인덱스 을 사용하고, 마지막 인덱스가 없으면 배열의 길이를 사용한다.
[a:b] 는 [a, b) 즉 a 는 포함하고 b 는 포함하지 않는다.

```python
mylist = ["List item 1", 2, 3.14]
print mylist[:] # [0:3] 과 같다
```
    ['List item 1', 2, 3.1400000000000001]
```python
print mylist[0:2]
```
    ['List item 1', 2]
```python
print mylist[-3:-1]
```
    ['List item 1', 2]

```python
>>> print mylist[1:]
```
    [2, 3.14]

```python
# 3 번재 인자로, 건너 띄면서 원소를 가지고 올 수도 있다.
# [::] == [::1] 가 기본이고, [::2] 로 step 이 2 이면 하나씩 건너뛴다.
print mylist[::2]
```
    ['List item 1', 3.14]

# 문자열(Strings)

string 은 "hello" 또는 'hello' 처럼, " 와 ' 를 아무것이나 사용해도 된다. "say 'hello'" 처럼 하나를 스트링 안쪽에 사용할 수도 있다. 여러줄에 걸친 string 은 따옴표 세개 (""") 를 사용한다. 파이썬은 u"이것은 unicode 문자열입니다" 의 형태로 Unicode 문자열을 기본 지원한다. % 연산자와 tuple 을 사용하여 문자열의 한 부분을 치환할 수 있다.

```python
print "Name: %s Number: %s String: %s" % (myclass.name, 3, 3 * "-")
```
    Name: Poromenos Number: 3 String: ---

```python
# 다음처럼 dictionary 를 사용하여 치환할 수도 있다.
print "This %(verb)s a %(noun)s." % {"noun": "test", "verb": "is"}
```
    This is a test.
    Flow control statements

if, for, while 을 이용하여 흐름을 제어한다. range() 를 이용하여 숫자 배열을 얻을 수 있다:

```python
rangelist = range(10)
print rangelist
```
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

```python
for number in rangelist:
    # number 가 tuple 안에 들어 있는지 확인한다
    if number in (3, 4, 7, 9):
        # "break" 로 "else" 문을 실행하지 않고 for 문을 나온다.
        break
    else:
        pass  # 아무것도 하지 않는다
```

```python
if rangelist[1] == 2:
    print "두번째 아이템이 2 이다"
elif rangelist[1] == 3:
    print "두번째 아이템이 3 이다"
else:
    print "Dunno"
```

```python
while rangelist[1] == 1:
    pass
```

## 함수(Functions)

함수는 `def` 키워드를 이용하여 선언한다. 함수의 인자중, 반드시 필요한 인자를 먼저 나열하고, 선택적 인자들을 그 후에 나열한다. 선택적 인자들에게는 기본값을 설정한다. 여러개의 값을 한꺼번에 tuple 로 리턴할 수 있다. Lambda 함수는 선언없이, 필요할 때 정의해서 사용하는 함수다. 인자는 레퍼런스 (참조) 로 전달된다. (역주: C++ 의 포인터가 카피되어 전달된다고 보면 된다, 전달된 변수를 수정하는 것이아니라, 새로운 값을 할당하면, 함수 바깥쪽에서는 이 변화는 인지하지 못한다.) 하지만 전달 받은 immutable 타입들 (튜플, int, string 등등) 은 참조로 전달되었다고 하더라도, 수정할 수 없다.

```bash
# 다음 문장은 def funcvar(x): return x + 1 와 같다.
funcvar = lambda x: x + 1
>>> print funcvar(1)
2

# an_int 와 a_string 은 선택적 인자로 기본값을 가진다.
def passing_example(a_list, an_int=2, a_string="A default string"):
a_list.append("A new item")
an_int = 4
return a_list, an_int, a_string

>>> my_list = [1, 2, 3]
>>> my_int = 10
>>> print passing_example(my_list, my_int)
([1, 2, 3, 'A new item'], 4, "A default string")
>>> my_list
[1, 2, 3, 'A new item']
>>> my_int
10

```

## Classes

파이썬은 제한적으로 다중 상속을 지원한다. private 변수와, 함수는 앞에 __ 을 붙인다. 관습일 뿐이며, python 언어 자체는 private 이란 개념이 없다.

```bash
# 클래스 객체를 만든다.
class MyClass(object):
common = 10
def __init__(self):
self.myvariable = 3
def myfunction(self, arg1, arg2):
return self.myvariable

>>> classinstance = MyClass()

>>> classinstance.myfunction(1, 2)
3
# 객체에서도 common 속성을 사용할 수 있다.
>>> classinstance2 = MyClass()
>>> classinstance.common
10
>>> classinstance2.common
10
# 클래스 변수를 변경한다
>>> MyClass.common = 30
>>> classinstance.common
30
>>> classinstance2.common
30
# classinstance 객체에 common 이라는 속성을 생성하고, 값을 준다
>>> classinstance.common = 10
>>> classinstance.common
10
>>> classinstance2.common
30
>>> MyClass.common = 50
# classinstance.common 은 객체의 속성이기 때문에 변하지 않는다.
>>> classinstance.common
10
>>> classinstance2.common
50

# MyClass 클래스를 상속받는다.
# class OtherClass(MyClass1, MyClass2, MyClassN) 형태로 다중상속 받을 수 있다.
class OtherClass(MyClass):
# "self" 인자는 자동으로 넘어오는 인자로 객체 자신을 가리킨다.
# 즉 self 를 이용하여 다음처럼 객체를 변경할 수 있다.
def __init__(self, arg1):
self.myvariable = 3
print arg1

>>> classinstance = OtherClass("hello")
hello
>>> classinstance.myfunction(1, 2)
3
# 이 클래스는 test 라는 변수를 정의한적이 없다.
# 하지만 다음 처럼 그냥 만들수 있다.
>>> classinstance.test = 10
>>> classinstance.test
10

```

## Exceptions

try-exept [exceptionname] 형태로 exception 을 처리한다:

```bash
def some_function():
try:
# 0 으로 나눠서 exception 을 발생시킨다.
10 / 0
except ZeroDivisionError:
print "Oops, invalid."
else:
# Exception 이 발생하지 않으면 일로 온다.
pass
finally:
# 위 코드들이 실행된 후에, 여기 finally 안의 코드들이 실행된다.
print "We're done with that."

>>> some_function()
Oops, invalid.
We're done with that.
Importing

```

라이브러리를 import [library_name] 으로 불러와 사용할 수 있다. from [library_name] import [name] 으로 라이브러리의 특정 이름만 가져올 수 있다:

```bash
import random # random library 를 불러온다
from time import clock # time 라이브러리의 clock 함수를 가져온다.

randomint = random.randint(1, 100)
>>> print randomint
64

```

## File I/O

파이썬은 다수의 내장 라이브러리를 제공한다. 다음 예제는 pickle 라이브러리를 이용하여 데이터를 serialize 하여 파일로 저장하는 것을 보여준다.

```bash
import pickle
mylist = ["This", "is", 4, 13327]
# C:binary.dat 파일을 쓰기 모드로 연다.
# 'r' 은 raw 라는 뜻으로, 가 escaping 을 의미하지 않도록 한다.
myfile = open(r"C:binary.dat", "w")
pickle.dump(mylist, myfile)
myfile.close()

# 파일을 읽어서 데이터를 로드한다
myfile = open(r"C:binary.dat")
loadedlist = pickle.load(myfile)
myfile.close()
>>> print loadedlist
['This', 'is', 4, 13327]

# 텍스트 파일에 데이터를 저장한다
myfile = open(r"C:text.txt", "w")
myfile.write("This is a sample string")
myfile.close()

myfile = open(r"C:text.txt")
>>> print myfile.read()
'This is a sample string'
myfile.close()

```

## Miscellaneous

1 < a < 3 같은 조건을 사용할 수 있다. del 키워드를 이용하여, 변수를 삭제하거나, 배열의 아이템을 삭제한다. list comprehension 을 이용하여 리스트를 만들 수 있다. list comprehension 은 for 와 if 문을 내부에 사용한다.

```bash
>>> lst1 = [1, 2, 3]
>>> lst2 = [3, 4, 5]
>>> print [x * y for x in lst1 for y in lst2]
[3, 4, 5, 6, 8, 10, 9, 12, 15]
>>> print [x for x in lst1 if 4 > x > 1]
[2, 3]

# 원소 하나라도 true 인지 확인한다.
>>> any([i % 3 for i in [3, 3, 4, 4, 3]]) # any(0,0,1,1,0)
True

# Check for how many items a condition is true.
>>> sum(1 for i in [3, 3, 4, 4, 3] if i == 4)
2
>>> del lst1[0]
>>> print lst1
[2, 3]
>>> del lst1

```

함수 바깥에 정의하는 변수는 글로벌 변수이다. 어디서도 이 변수를 접근할 수 있지만, 이 값을 함수내에서 변경할 때에는 global 키워드를 사용하여 선언해줘야 한다. 그렇지 않으면, 파이썬은 같은 이름의 새로운 로컬 변수를 만든다.

```python
number = 5

def myfunc():
# 5 를 출력한다.
print number

def anotherfunc():
# execption 을 발생시킨다:
# 파이썬은 이 함수에서 number 가 사용될 것을 알고, 로컬 객체를 만든다.
# 그런데 이 변수에 값을 설정하기 전에 print 하려고 해서 에러가 발생한다.
print number
number = 3

def yetanotherfunc():
global number
# global 변수를 수정한다.
number = 3

```

## Epilogue

파이썬의 모든 것을 다룬 것은 물론 아니다. 파이썬은 방대한 라이브러리를 제공하며, 더 많은 내용을 배우려면 Dive Into Python 같이 좋은 책을 이용하기 바란다. python 을 접하는데 도움이 되었으면 한다.