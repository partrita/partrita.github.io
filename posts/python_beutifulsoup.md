<!--
.. title: BeautifulSoup을 사용해 웹 스크래핑하기
.. slug: python_beutifulsoup
.. date: 2015-09-13 17:36:21 UTC+09:00
.. tags: Python, BeautifulSoup, Web, Web Scraping
.. category: python
.. link: 
.. description: 
.. type: text
-->

시사용어 모음집은 유료 서비스(예를 들면 *에듀스*)를 이용할 수 밖에 없었는데 [단비뉴스](http://www.danbinews.com/)라는 곳에서 감사하게도 시사용어를 소개하고 있는 페이지가 있어 파이썬을 사용해 초간단 웹 스크래핑을 했습니다.

# 1. 필요한 것
* python 2.7+
* BeautifulSoup 모듈

# 2. Code

```python

# -*- coding: utf-8 -*-
import urllib
from bs4 import BeautifulSoup

#결과는 results.txt파일에 저장
results = open('results.txt','a')
#스크래핑 실패한 페이지 리스트
fail_list = []

#가장 최근 페이지가 6013, 숫자를 1씩 줄이면서 스크래핑
for i in range(6013, 0, -1):
#스크래핑 할 페이지 주소
    url = 'http://www.danbinews.com/news/articleView.html?idxno='+ str(i)
    try:
        html = urllib.urlopen(url)
        soup = BeautifulSoup(html, "lxml")
        #아티클의 제목: class가 view_t인것
        title = soup.find('td',class_='view_t').get_text().strip()
        # '##'를 제목 앞에 추가해서 마크다운 포멧으로 바꾸고 인코딩 변환
        title2 = '## '+ title.encode('utf-8') +'n'
        #아티클의 내용 찾기 : class id가 view_r 인것
        text = soup.find('td',class_ ='view_r')
        #불필요한 광고를 제거 하기 위해 p tag안 내용만 선택
        text2 = text.find_next('p').get_text()
        #인코딩과 마지막에 줄바꿈 추가
        text3 = text2.encode('utf-8') + 'n'
        #결과 파일에 제목 쓰기
        results.write(title2)
        #결과 파일에 내용 쓰기
        results.write(text3)
        #스크래핑 성공 메시지 출력
        print 'Success : '+ str(i) + 'th article'
    except:
        #URL이 없는 경우 스크래핑 실패 출력
        print 'Fail : ' + str(i) + 'th article'
        #실패 리스트에 추가
        fail_list.append(i)

    #close the results file
    results.close()
#스크래핑 끝나면 출력
print 'Finished'기
print 'Fail list : '
print fail_list # 실패한 페이지 출력

```

# 3. 결과 확인

결과는 **result.txt** 파일에 저장됩니다.
> 파일은 금방 만들었는데 언제 다 읽나.