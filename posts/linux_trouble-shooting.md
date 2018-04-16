<!--
.. title: Linux trouble shooting
.. slug: linux-trouble-shooting
.. date: 2015-10-11 11:11:03 UTC+09:00
.. tags: Linux, trouble
.. category: Linux
.. link: 
.. description: 리눅스 문제 해결
.. type: text
-->

# 리눅스 해상도 문제 해결하기

구형 컴퓨터에 리눅스(리눅스 민트)를 설치하였습니다. 저해상도로 고정되는 경우는 처음이었는데, 검색을 통해 아래와 같은 방법으로 해결했습니다.

1. 먼저 아래와 터미널에 아래와 같은 명령어를 칩니다. (예시로 1600×900을 사용했는데, 원하는 비율로 변경하시면 됩니다.)

```bash
cvt 1600 900
```
    1600x900 59.95 Hz (CVT 1.44M9) hsync: 55.99 kHz; pclk: 118.25 MHz
    Modeline "1600x900_60.00" 118.25 1600 1696 1856 2112 900 903 908 934 -hsync +vsync

2. 위에서 얻은 결과를 참고해 모니터 설정을 추가 합니다. 위의 결과의 뒷부분을 복사해서 붙여넣으면 됩니다.
    - 모니터 마다 결과가 다르니 꼭 1번단계를 통해 직접 명령어를 만들어야 합니다.

```bash
xrandr --newmode "1600x900_60.00" 118.25 1600 1696 1856 2112 900 903 908 934 -hsync +vsync
# 새로운 모드를 만들고 아래와 같이 추가해줍니다.
xrandr --addmode VGA1 "1600x900_60.00"
```
면이 깜박이면서 1600×900해상도가 새롭게 생깁니다. 하지만 재부팅을하면 다시 복구가 되므로 매번 명령어를 입력하는 불편이 있습니다.

3. 쉘 스크립트(fix-resolution.sh)를 작성합니다. 텍스트에디터로 만들어서 확장자만 변경하시면 됩니다.

```bash
#!/bin/sh
# fix-resolution.sh
xrandr --newmode "1600x900_60.00" 118.25 1600 1696 1856 2112 900 903 908 934 -hsync +vsync
xrandr --addmode VGA1 "1600x900_60.00"
xrandr --output VGA1 --mode "1600x900_60.00"
```
4. fix-resolution.desktop라는 파일도 만들어 줍니다.

```bash
# fix-resolution.desktop
[Desktop Entry]
Type=Application
Name=fix-resolution.desktop
Exec=/usr/local/bin/fix-resolution.sh
```
5. 두개의 파일이 들어있는 디렉토리에서 터미널을 열고 다음의 명령어를 입력 합니다.

```bash
cp fix-resolution.sh /usr/local/bin
chmod +x /usr/local/bin/fix-resolution.sh
cp fix-resolution.desktop /etc/xdg/autostart
```
파일을 복사해서 옮겨주는 것이라서, 생성하신 파일은 이제 삭제하셔도 됩니다.


# 자주 사용하는 커맨드 Alias 만들기

터미널을 자주 사용하다보면 명령어 입력이 번거로울 때가 있습니다. 이럴 때를 위해서 Bash shell에서는 `Alias`라는 기능을 제공하고 있습니다. 기능을 사용하기 위해서는 `~/.bashrc` 파일의 수정이 필요합니다.

1. bashrc 파일 열기
```bash	
nano ~/.bashrc
```
nano 에디터로 파일을 열어줍니다.

2. Alias 명령어 추가하기
Alias 사용법은 다음과 같습니다. 
```
alias l="ls -a"
```
‘l’을 치면 ‘ls -a’랑 같은 효과가 나도록 설정하였습니다. 이제 Ctrl+x를 눌러 파일을 저장합니다.

3. Bash shell 재실행
저장한 내용을 적용하기 위해 shell을 다시 실행 해야합니다.

```bash
source .bashrc
```

이제 'l'을 누르면 적용이 된것을 확인 할 수 있습니다.