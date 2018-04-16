<!--
.. title: 파이썬으로 웹페이지 단어 세기
.. slug: python_wordcount
.. date: 2015-10-26 17:19:31 UTC+09:00
.. tags: Web, Python 
.. category: python
.. link: 
.. description: 웹페이지에 반복되는 단어를 세어 봅니다.
.. type: text
-->

파이썬을 사용하여 위키피디아 검색어를 입력하고 나온 결과 페이지의 글자수를 세어주는 스크립트 입니다.[데이터 과학자, 무엇을 배울 것인가](http://jpub.tistory.com/420)라는 책에서 코드를 가져와서 조금 수정 하였습니다.

```python
# -*- coding: utf-8 -*-
# 파이썬2.7 버전 기준으로 작성되어있음
import urllib2

# 접속할 URL
base_url = 'http://ko.wikipedia.org/wiki/'
# 사용자 에이전트
ua = 'Mozilla/5.0(Windows NT 6.1; WOW64) AppleWebKit/535.7(KHTML,like Gecko) Chrome/16.0.912.75 Safari/535.7'
# 취득하고 싶은 항목
queries = ['포유류', '파충류', '조류', '어류', '양서류']

result = {}
# URL의 내용 취득하기

for q in queries:
    # URL 인코딩하기
    url = base_url + urllib2.quote(q)
    # Request 객체 작성하기
    req = urllib2.Request(url, headers={'User-Agent': ua})
    try:
        # 리퀘스트 열기
        html = urllib2.urlopen(req).read()
        # 결과의 문자 수를 result에 부여하기
        result[q] = len(html)
    # HTTP 에러 시의 예외 처리
    except urllib2.HTTPError, e:
        print 'HTTP 에러'
        print '에러 코드: ', e.code
    # URL 에러 시의 예외 처리
    except urllib2.URLError, e:
        print 'URL 에러'
        print '이유: ', e.reason

# 각 항목의 문자 수를 표시하기
# 단어수가 많은 것으로 정렬
ord_result = sorted(result.items(), key=lambda x: x[1], reverse=True)
for q in ord_result:
    print('쿼리：' + q[0] + ', 문자 수：' + str(q[1]))

```

# 실행 결과

실행하면 아래와 같이 각각의 쿼리와 문자수를 확인할 수 있습니다.

    쿼리：어류,문자 수：286300
    쿼리：포유류,문자 수：94588
    쿼리：양서류,문자 수：77480
    쿼리：파충류,문자 수：73183
    쿼리：조류,문자 수：21144

