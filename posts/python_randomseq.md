<!--
.. title: 랜덤하게 단백질 서열만들기
.. slug: python_randomseq
.. date: 2015-05-11 17:28:23 UTC+09:00
.. tags: Python, Random
.. category: python
.. link: 
.. description: 임의의 서열을 만들어봅니다.
.. type: text
-->

랜덤으로 원하는 길이의 단백질 서열을 원하는 만큼 만드는 파이썬 스크립트 입니다.

```python
# python 2.7 버전
# -*- coding: utf-8 -*-
from random import Random

def AminoacidGenerator(number, length):
	print '***generate random aminoacid sequence ***'
	codeFile = open('codes.txt', 'w')
	if number <= 0:
		return 'invalid number of protein'
	else:
		aminoacid = 'ACDEFGHIKLMNPQRSTVWY'		
		random = Random()
		for j in range(1, number + 1):
			str = ''
			for i in range(1, length+1):
				index = random.randint(1,len(aminoacid))
				str = str + aminoacid[index -1]
			codeFile.write(str+'\n')

# 100개 길이의 단백질 서열을 100개 만들어 봅니다. 
print AminoacidGenerator(100, 100)
```

그냥 재미로 만들어 보았습니다. 만들어진 서열을 **NCBI**의 **BLAST!** 검색에 넣어보았는데, 비슷한 서열이 검색되지는 않더군요. 그 방대한 데이터베이스에서 겹치는 서열이 없다니 진화의 놀라움에 대해 다시 생각해보게 되는군요.