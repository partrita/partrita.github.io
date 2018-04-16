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

------------

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

------------

# 한글로 된 압축파일명이 깨지는 경우

윈도우에 많이 사용 되는 압축파일인 `.zip`포멧은 리눅스에서 인코딩 문제로 자주 파일명이 깨집니다. 이러한 문제를 해결하려면 터미널 명령어 `unzip`에 인코딩 옵션을 줘야 합니다.

1. unzip 사용법
명령어의 사용법은 다음과 같습니다.
```bash
$unzip -O [인코딩] [파일명]
```
윈도우에서 많이 사용되는 인코딩은 cp949이므로, 아래와 같이 쓰면 됩니다.
> 물론 인코딩을 미리 확인하고 사용하는게 좋습니다.

터미널에 아래와 같이 입력하세요.
```bash
$unzip -O cp949 한글.zip
```

위 방법을 이용하면 인코딩 깨짐 없이 무사히 압축을 해제할 수 있습니다.

2. 이 모든 삽질의 원인
zip파일은 거의 모든 압축포맷 중에 단연 최고의 사용률을 자랑하는 포맷입니다. 하지만 치명적인 단점이 있는데 바로 Unicode가 지원되지 않는 다는 것이죠. 그래서 인코딩이 깨지는 현상이 발생하게 되는 것입니다. 앞으로는 `7z`와 같은 새로운 압축 포맷을 사용하는게 좋겠습니다.

------------

# 터미널에서 컴퓨터 하드웨어 정보 확인하기


1. 리눅스 버전확인

```bash
~$ cat /etc/issue
```
    Ubuntu 15.04

사용중인 리눅스의 버전을 확인합니다.

2. 하드디스크 용량 확인

```bash
~$ df -h
```
    Filesystem Size Used Avail Use% Mounted on
    udev 3.8G 0 3.8G 0% /dev
    tmpfs 771M 26M 746M 4% /run
    /dev/sda5 33G 15G 17G 46% /
    tmpfs 3.8G 604K 3.8G 1% /dev/shm
    tmpfs 5.0M 4.0K 5.0M 1% /run/lock
    tmpfs 3.8G 0 3.8G 0% /sys/fs/cgroup
    cgmfs 100K 0 100K 0% /run/cgmanager/fs
    tmpfs 771M 48K 771M 1% /run/user/1000

3번째 줄에서 총 공간이 총 33G이고 15G를 사용하고 있음을 확인합니다.

3. CPU 코어 갯수 확인

```bash
~$ cat /proc/cpuinfo | grep processor | wc -l
```
    8
코어의 갯수가 8개 임을 알수 있습니다.

4. 램 사용량 확인

```bash
~$ free -m
```
    total used free shared buffers cached
    Mem: 7708 2690 5017 161 351 669
    -/+ buffers/cache: 1669 6038
    Swap: 0 0 0

전체 7708Mb에서 2618Mb를 사용하고 있습니다.

-----------

# 헐리우드 해커 터미널

영화에 나오는 해커처럼 터미널에 복잡한것을 띄워 봅시다. 아래 코드를 터미널에 입력하면 랜덤하게 hex dump가 시작됩니다. 

```bash
hexdump -C /dev/urandom | GREP_COLOR='1;32' grep --color=auto 'ca fe'
```
> hex dump는 램 또는 파일이나 저장장치에 있는 컴퓨터 데이터의 십육진법적인 보임새이다. 데이터의 hex dump를 보는 것은 주로 디버깅이나 리버스 엔지니어링의 한 부분이다.  -- 위키피디아

이와 비슷한 것으로 영화 **메트릭스**에 나오는 화면도 시도해 보겠습니다.

```bash
# 먼저 cmatrix를 설치해야 합니다.
sudo apt-get install cmatrix
# 실행합니다.
cmatrix
```

별 의미는 없지만 흥미롭습니다.

--------------

# 죽은 프로세서 되살리기

서버 관리를 하다 보면, 죽으면 안되는 데몬이 갑자기 죽는 경우가 있다. 이런 경우를 대비해 데몬이 죽었으면 재 실행 시켜 주는 스크립트를 만들어 보겠습니다.

1. 쉘 스크립트 작성
아파치 데몬이 죽었을 경우 자동 재 시작하는 스크립트를 작성해보겠습니다. 아래와 같은 내용의 쉘 스크립트 파일을 만듭니다. 파일명은 `revive.sh`로 하겠습니다.

```bash
# revive.sh
#!/bin/bash
http="`pgrep http  | wc -l`"
if [ "$http" -eq "0" ] ; then
/usr/local/apache/bin/apachectl restart
fi
```
`http`라는 변수에 `pgrep http`로 아파치 프로세서의 갯수를 세어 저장합니다. 그리고, `if`문에서 `http`변수에 들어 있는 값이 0이라면 아파치를 재시작 합니다. 위의 스크립트를 `revive.sh` 로 저장하고, 터미널에 다음과 같이 입력합니다.

```bash
$ chmod -x revive.sh
```
이는 퍼미션을 주기 위한 것입니다.

2. 크론(cron)에 등록해서 1분마다 확인하기
리눅스에서는 정기적으로 반복되는 작업을 위한 `cron`이라는 서비스가 있습니다. 크론으로 1분에 한번씩 위의 스크립트가 작동되도록 하겠습니다. 

```bash
crontab -e
```
으로 크론을 실행한뒤 아래와 같이 입력합니다.

```
* * * * * su - root -c '/root/revive.sh /dev/null'
```
파일을 저장한뒤 적용을 위해서는 로그오프가 필요합니다. 

------------------------

# 우분투 단축키 모음

1. General keyboard shortcuts 
    - Ctrl + A = Select all
    - Ctrl + C = Copy the highlighted content to clipboard
    - Ctrl + V = Paste the clipboard content
    - Ctrl + N = New (Create a new document, not in terminal)
    - Ctrl + O = Open a document
    - Ctrl + S = Save the current document
    - Ctrl + P = Print the current document
    - Ctrl + W = Close the close document
    - Ctrl + Q = Quit the current application
2. Keyboard shortcuts for GNOME desktop
    - Ctrl + Alt + F1 = Switch to the first virtual terminal
    - Ctrl + Alt + F2(F3)(F4)(F5)(F6) = Select the different virtual terminals
    - Ctrl + Alt + F7 = Restore back to the current terminal session with X
    - Ctrl + Alt + Backspace = Restart GNOME
    - Ctrl + Alt + L = Lock the screen.
    - Alt + Tab = Switch between open programs
    - Alt + F1 = opens the Applications menu
    - Alt + F2 = opens the Run Application dialog box.
    - Alt + F3 = opens the Deskbar Applet
    - Alt + F4 = closes the current window.
    - Alt + F5 = unmaximizes the current window.
    - Alt + F7 = move the current window
    - Alt + F8 = resizes the current window.
    - Alt + F9 = minimizes the current window.
    - Alt + F10 = maximizes the current window. 
    - Alt + Space = opens the window menu.
    - Ctrl + Alt + + = Switch to next X resolution
    - Ctrl + Alt + - = Switch to previous X resolution
    - Ctrl + Alt + Left/Right = move to the next/previous workspace
3. Keyboard shortcuts for Terminal
    - Ctrl + A = Move cursor to beginning of line
    - Ctrl + E = Move cursor to end of line
    - Ctrl + C = kills the current process.
    - Ctrl + Z = sends the current process to the background.
    - Ctrl + D = logs you out.
    - Ctrl + R = finds the last command matching the entered letters.
    - Enter a letter, followed by Tab + Tab = lists the available commands beginning with those letters.
    - Ctrl + U = deletes the current line.
    - Ctrl + K = deletes the command from the cursor right.
    - Ctrl + W = deletes the word before the cursor.
    - Ctrl + L = clears the terminal output
    - Shift + Ctrl + C = copy the highlighted command to the clipboard.
    - Shift + Ctrl + V (or Shift + Insert) = pastes the contents of the clipboard.
    - Alt + F = moves forward one word.
    - Alt + B = moves backward one word.
    - Arrow Up/Down = browse command history
    - Shift + PageUp / PageDown = Scroll terminal output 
4. Keyboard shortcuts for Compiz
    - Alt + Tab = switch between open windows
    - Win + Tab = switch between open windows with Shift Switcher or Ring Switcher effect
    - Win + E = Expo, show all workspace
    - Ctrl + Alt + Down = Film Effect
    - Ctrl + Alt + Left mouse button = Rotate Desktop Cube
    - Alt + Shift + Up = Scale Windows
    - Ctrl + Alt + D = Show Desktop
    - Win + Left mouse button = take screenshot on selected area
    - Win + Mousewheel = Zoom In/Out
    - Alt + Mousewheel = Transparent Window
    - Alt + F8 = Resize Window
    - Alt + F7 = Move Window
    - Win + P = Add Helper
    - F9 = show widget layer
    - Shift + F9 = show water effects
    - Win + Shift + Left mouse button = Fire Effects
    - Win + Shift + C = Clear Fire Effects
    - Win + Left mouse button = Annotate: Draw
    - Win + 1 = Start annotation
    - Win + 3 = End annotation
    - Win + S = selects windows for grouping
    - Win + T = Group Windows together
    - Win + U = Ungroup Windows
    - Win + Left/Right = Flip Windows
5. Keyboard shortcut for Nautilus
    - Shift + Ctrl + N = Create New Folder
    - Ctrl + T = Delete selected file(s) to trash
    - Alt + ENTER = Show File/Folder Properties
    - Ctrl + 1 = Toggle View As Icons
    - Ctrl + 2 = Toggle View As List
    - Shift + Right = Open Directory (Only in List View)
    - Shift + Left = Close Directory (Only in List View)
    - Ctrl + S = Select Pattern
    - F2 = Rename File
    - Ctrl + A = Select all files and folders
    - Ctrl + W = Close Window
    - Ctrl + Shift + W = Close All Nautilus Windows
    - Ctrl + R = Reload Nautilus Window
    - Alt + Up = Open parent directory
    - Alt + Left = Back
    - Alt + Right = Forward
    - Alt + Home = go to Home folder
    - Ctrl + L = go to location bar
    - F9 = Show sidepane
    - Ctrl + H = Show Hidden Files
    - Ctrl + + = Zoom In
    - Ctrl + - = Zoom Out
    - Ctrl + 0 = Normal Size 

------------------------

# 리눅스를 노트북에 사용할때

리눅스를 노트북에 최적화 시키는 툴에 [TLP]()가 있습니다. TLP 는 리눅스 배포판과 하드웨어를 자동으로 인식해 노트북의 전원관리와 여러 트윅을 적용 시켜주기 때문에 아주 편리합니다. 다음과 같은 기능이 있습니다.

1. 배터리와 AC전원 유무에 따라 변경되는 효과
    - Kernel laptop mode and dirty buffer timeouts;
    - Processor frequency scaling including "turbo boost" / "turbo core";
    - Power aware process scheduler for multi-core/hyper-threading;
    - Hard disk advanced power management level and spin down timeout (per disk);
    - SATA aggressive link power management (ALPM);
    - PCI Express active state power management (PCIe ASPM) – Linux 2.6.35 and above;
    - Runtime power management for PCI(e) bus devices – Linux 2.6.35 and above;
    - Radeon KMS power management – Linux 2.6.35 and above, not fglrx;
    - Wifi power saving mode – depending on kernel/driver;
    - Power off optical drive in drive bay (on battery).
2. 추가적인 TLP 기능:
    - I/O scheduler (per disk);
    - USB autosuspend with blacklist;
    - Audio power saving mode – hda_intel, ac97;
    - Enable or disable integrated wifi, bluetooth or wwan devices upon system startup and shutdown;
    - Restore radio device state on system startup (from previous shutdown);
    - Radio device wizard: switch radios upon network connect/disconnect and dock/undock;
    - Disable Wake On LAN;
    - WWAN state is restored after suspend/hibernate;
    - Undervolting of Intel processors – requires kernel with PHC-Patch;
    - Battery charge thresholds – ThinkPads only;
    - Recalibrate battery – ThinkPads only.

## 설치법
1. 충돌을 일으킬 수 있는 laptop-mode 제거
```bash
sudo apt-get purge laptop-mode-tools
```
2.  TLP설치
```bash
sudo add-apt-repository ppa:linrunner/tlp
sudo apt-get update
sudo apt-get install tlp
```
3. 처음 실행후에는 부팅시 자동 실행된다.
```bash
sudo tlp start
```

--------------------
