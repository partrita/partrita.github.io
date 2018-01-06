.. title: hello world
.. slug: hello-world
.. date: 2017-12-11 20:20:47 UTC+09:00
.. tags: 
.. category: 
.. link: 
.. description: This is the first post
.. type: text

Hello world!
==============
첫 번째 포스트 이자, 처음으로 써보는 **reStructuredText** 포멧입니다. 

리스트 만들기
-----------------

- A bullet list item
- Second item

  - A sub item

- Spacing between items creates separate lists

- Third item

1) An enumerated list item

2) Second item

   a) Sub item that goes on at length and thus needs
      to be wrapped. Note the indentation that must
      match the beginning of the text, not the 
      enumerator.

      i) List items can even include

         paragraph breaks.

3) Third item

#) Another enumerated list item

#) Second item

이미지
-----------------
.. image:: https://geekpete.com/blog/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-3.19.27-pm.png

하이퍼링크
-----------------
A sentence with links to Wikipedia_ and the `Linux kernel archive`_.

.. _Wikipedia: https://www.wikipedia.org/
.. _Linux kernel archive: https://www.kernel.org/

Another sentence with an `anonymous link to the Python website`__.

__ https://www.python.org/

N.B.: named links and anonymous links are enclosed in grave accents (`), and not in apostrophes (').

코드 블럭
-----------------
::

  some literal text

This may also be used inline at the end of a paragraph, like so::

  some more literal text

.. code:: python

   print("A literal block directive explicitly marked as python code")

