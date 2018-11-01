.. title: 정규직으로 줄바꿈 제거하기
.. slug: regular-exp_blank
.. date: 2015-04-14 18:40:03 UTC+09:00
.. tags: text editor, sublimetext, visual studio code, atom
.. category: Regular Expression 
.. link: 
.. description: 
.. type: text

간혹보면 가독성을 위해 엔터키를 마구쳐 내려간 글들이 있습니다.보기엔 좋지만, 출력할때는 많이 불편합니다. 그럴땐 '찾아 바꾸기' 기능을 이용해 해결할 수 있습니다. 물론 정규식을 지원하는 에디터에서 말입니다. Sublimetext, visual studio code, atom 등등의 에디터에서 다음을 실행해 보세요.

.. image:: http://i1.wp.com/blog.singihae.com/wp-content/uploads/sites/2/2014/02/sublime-text.png
   :align: center 

1. `Ctrl + H`를 누른 후 (or Find > Replace)에 입력 창에 `^\n`을 입력한다. 
2. “regular expression”을 선택한다. (Alt + R을 누르거나 [.*] 아이콘을 클릭)
3. 그리고 Replace All를 누르면 모든 줄 바꿈이 삭제 됩니다.
