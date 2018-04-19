<!--
.. title: 파이썬 리스트 중복 아이템 제거
.. slug: python_duplicate_list
.. date: 2013-05-06 17:30:49 UTC+09:00
.. tags: Python
.. category: python
.. link: 
.. description: 리스트에 중복된 아이템을 제거하는 방법
.. type: text
-->

Python의 리스트에 중복된 아이템은 아래와 같은 방법으로 쉽게 제거할 수 있습니다.

```python
#리스트 생성과 확인
li = ["a","b","c","d","a","b"]
print('li')
```
    ["a","b","c","d","a","b"]

```python
#리스트에 중복 아이템 제거
li = list(set(li))
print(li)
```
    ['a', 'c', 'b', 'd']

