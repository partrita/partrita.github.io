<!--
.. title: Walking the file tree
.. slug: walking-the-file-tree
.. date: 2015-04-16 16:10:58 UTC+09:00
.. tags: Python, os.walk, DIRwalk
.. category: python
.. link: 
.. description: Walking the file tree
.. type: text
-->

현재 디렉토리 아래의 모든 파일(서브디렉토리 포함) 목록을 얻고자 할 때는 `os.walk('./')`를 호출해서 이터레이션 하면서 튜플의 3번째 리스트만 살펴보면 됩니다. 아래의 예제 코드와 확인하세요. 

```python
# python 2.7 버전
import os
for root, dirs, files in os.walk('./'):
    for file in files:
        print file
```
이런 식으로 호출하면 모든 파일 이름이 표시됩니다.

# os.walk

`os.walk`는 특정 디렉토리 아래의 모든 디렉토리와 파일의 목록을 얻어 올 수 있도록 도와줍니다. for 루프에서 3개의 아이템으로 구성된 튜플로 분해가 가능한데 이름만으로도 무엇인지 알 수 있습니다. **root**는 어떤 디렉토리인지, **dirs**는 root 아래의 디렉토리 목록, 그리고 **files**는 root 아래의 파일 목록이다. 모든 목록은 리스트 형태입니다. 좀 더 많은 기능은 [공식 문서](https://docs.python.org/2/library/os.html)를 참고하세요.


# 스크립트 파일 예제

아래와 같이 스크립트 파일을 만들어 사용해 보았습니다.

```python
#-*- coding: utf-8 -*-
# sub_dir_search.py
# python 2.7 버전
import os
from datetime import datetime

now = datetime.now()
nowDate = now.strftime('%Y%m%d') # 오늘날짜

def allfiles2(path):
    res = []
    for root, dirs, files in os.walk(path):
        rootpath = os.path.join(os.path.abspath(path), root)
        for file in files:
            filepath = os.path.join(rootpath, file)
            res.append(filepath)
        with open(nowDate+'_list.txt', 'w') as f:
            # 오늘날짜_list.txt 파일을 생성합니다.
            for ress in res:
                f.write(ress+'\n')
            
def main():
    x = raw_input('where to search? : ')
    # 검색할 곳의 위치를 물어봅니다.
    allfiles2(x)

if __name__ == '__main__':
    main()
```

루트 폴더('C:\')를 넣었더니 엄청나게 큰 파일 생성되었습니다.
