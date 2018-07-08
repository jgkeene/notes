Misc
####

.. contents::
  :local:
  :depth: 5

Linux Commands    
========

rsync
-----

.. code-block:: bash

  rsync --verbose --recursive --times --partial-dir=/home/azhee/.rsync-partial --info=progress2 SOURCE DEST


find
-----

.. code-block:: bash

  find . -name "*.mp3" | grep -o '.*/' | sort | uniq
  find . -type f \( -name "*.py" -o -name "*.txt" \)

grep
-----

.. code-block:: bash
  
  grep -n SEARCHTERM FILE


Linux Tasks
==========
- add/del/mod user
- grant user sudo permission (sudoers)
- chmod/chown/file permissions


Ubuntu
======

Capslock
-------------
- `(source) <http://www.noah.org/wiki/CapsLock_Remap_Howto>`_
- `(source) <https://help.ubuntu.com/community/NumLock>`_
- `(source) <https://help.ubuntu.com/community/NumLock>`_

# Numbering files (appended number)
for i in *.png
do
  mv $i ${i/.png/-0}
done

# Numbering files (prepended number)
for i in {1..9}
do
  mv file_$i `printf file_0$i`
done

# Monitor the job
watch -c -d -n 1 tail /var/log/syslog

# Downlaod a file
curl URL --output FILE

# DownloadURL  multiple files matching a patterns
curl URL 2> /dev/null |
  grep -iE '(FUCK|YOU)' |
  sed -E 's/^.*href="(.*)".*$/\1/' |
  while read line; do
  echo "http://www.whyprime.com/temp/destroy_all_software/"$line
  done

# Print the nth word (awk treats whitespace as word delimeters)
awk '{print $1}'

# image to pdf
convert IMAGEFILE{1..3}.jpg OUT.pdf
# txt to pdf
soffice --headless --convert-to pdf in.txt
# pdf to txt
pdftotext IN.pdf OUT.txt
# combine pdfs
pdfunite ./*.pdf OUT.pdf
# grep pdfs, recursively
pdfgrep -HiR 'pattern' /path
# giff pdfs
pdfdiff FILE1.pdf FILE2.pdf


Samba Windows Shares
--------------------
Install CIFS VFS (http://www.configserverfirewall.com/ubuntu-linux/mount-samba-share-ubuntu-cifs/)
sudo apt install cifs-utils
# Manual mount via Nautilus
nautilus --select smb://192.168.0.3/nfs
# Results
mount | grep gvfsd-fuse
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)
# Automatic mount, via fstab
mkdir /media/azhee/nfs
sudo vim /etc/fstab
//192.168.0.3/nfs  /media/azhee/nfs  cifs  rw,_netdev,username=0,password=0,users  0 0 
mount | grep cifs
//192.168.0.3/nfs on /media/azhee/nfs type cifs (rw,nosuid,nodev,relatime,vers=default,cache=strict,username=0,domain=,uid=1000,forceuid,gid=1000,forcegid,addr=192.168.0.3,file_mode=0755,dir_mode=0755,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,echo_interval=60,actimeo=1,_netdev)


Manpages
--------
# Browse with yelp **(best for navigating links)**
yelp man:grep
# Generate html manpage with groff, open with browser **(best for printing)**
sudo apt install groff
man --html=google-chrome-stable SOME_APPLICATION

Pipe html directly to browser

.. code-block:: bash

# Install txt2html
sudo apt install txt2html
# Pipe manpage to browser
man SOME_APPLICATION | txt2html - | google-chrome-stable "data:text/html;base64,$(base64)"

Pipe to lynx, browse with navigation links

.. code-block:: bash

# Install man2html
sudo apt install man2html
# Pipe manpage to lynx
zcat $(man --path 1 grep) | man2html -l | lynx -stdin
# Pipe manpage to w3m
zcat $(man --path 1 grep) | man2html -l | w3m -T text/html

View Files From A Clonezilla Backup
-----------------------------------
# Extract into an image file
sudo su
cat sda2.ext4-ptcl-img.gz.* | gunzip -c | partclone.restore -s - -W -o./sda2.img
# Mount the image file and browse files

Dconf Settings
--------------

.. code-block:: bash

# dump dconf settings
dconf dump / >> ./dump.txt
# restore dconf settings
dconf load ./dump.txt

Other Ubuntu Software
---------------------

- ThinkingRock (GTD) `shell script installer <https://trgtd.com.au/index.php/component/rsfiles/download?path=v3.7.0%252FTrial%252FLinux%252Ftr-3.7.0-trial-jre64.sh>`_

View Installed Software 
-----------------------

.. code-block:: bash

# List all installed packages, with version numbers
apt list --installed

# Lists installed packages (excludes if installed as a dependency), with descriptions
aptitude search '~i!~M'

# Lists installed packages (excludes if installed as a dependency), without descriptions
aptitude search -F '%p' '~i'

# Shows the installation commands you used, with dates
(zcat $(ls -tr /var/log/apt/history.log*.gz); cat /var/log/apt/history.log) 2>/dev/null |
egrep '^(Start-Date:|Commandline:)' |
grep -v aptdaemon |
egrep -B1 '^Commandline:'

# Shows the installation commands you used, without dates
(zcat $(ls -tr /var/log/apt/history.log*.gz); cat /var/log/apt/history.log) 2>/dev/null |
egrep '^(Start-Date:|Commandline:)' |
grep -v aptdaemon |
egrep '^Commandline:'


Vim
===

Opening files from shell

.. code-block:: bash

# Open in tabs
vim -p FILE FILE FILE

# Open in splits
vim -O FILE FILE FILE

Important commands

.. code-block:: text

daw                 " Deleteword, better than 'dw'
I                   " Begin of line, better than '0i'
yiw                 " Copy word you're in
mm -> `m            " Mark cursor pos. as 'm' -> goto mark 'm'

ctrl-w h            " Move split left
ctrl-w l          " Move split right

bo sp       " Split horizontally across all windows

z <cr>      " Bring cursor position and screen to top of window

z-R                   " Open all folds
z-M                       " Close all folds

g;                    " Goto prev edit position
g,                    " Goto next edit position
changes             " List all edit positions

=                     " Auto-indent selected lines
gg -> =G            " Auto-indent all lines

ctrl-pgUp             " Goto next tab
ctrl-pgDown           " Goto prev tab

:set list         " Show hidden chars (tabs, spaces, etc..)
:set nolist     " Hide hidden chars (tabs, spaces, etc..)

:set colorcolumn=79       " Draw vertical column

:set colorscheme?     " Check a setting 

%s/^M$//g                 " Remove ^M chars (to get ^M in vim, type c-V -> c-M)

qd                    " Start recording macro to register d (possible registers are [a-z])
q                     " Stop recording macro
@d                    " Execute your macro
@@                    " Execute your macro again
'<,'>normal @d        " Execute your macro on a visual selection

dt<           " Delete till a char (ex: '<')

=                     " Auto-indent selected lines
gg =G                 " Auto-indent all lines

tabedit FILE    " Open file into a new-tab

yO -> (paste)         " Paste and preserve formatting

'{' & '}'             " Jump through paragraphs
'(' & ')'             " Jump through sentences
%                     " Jump between braces/parens/etc

g/^$/d                  " Delete empty lines in insert mode
'<,'>g/^$/d             " Delete empty lines in visual mode

:/\s\+$/        " Hilight whitespace chars

:set ff=unix        " Convert a Windows file into a unix file

Low-level
=========

.. code-block:: bash

stdout | pacat          # https://www.youtube.com/watch?v=GtQdIYUtAHgs
pacat /dev/urandom > padsp
strace            # See the system calls made by an program
hopper              # Disassembler
xxd -s 0x7f0000 -g 1 mbp101_b02.rom | head -15    # Hex viewer
binwalk -E [filename]             # File etropy viewer
strings -n 4 -t x FILE        # Find string in a binary file
zmap            # Nmap on steroids

Mac address spoofing
--------------------

.. code-block:: bash

# Via command line
ip link show interface
ip link set dev interface down
ip link set dev interface address XX:XX:XX:XX:XX:XX
ip link set dev interface up

#Via GUI
macchanger

Steganography
-------------

Youtube presentations `1 <https://www.youtube.com/watch?v=_j1LWehywgc>`_ `2 <https://www.youtube.com/watch?v=BcDbKlz06no>`_ `3 <https://www.youtube.com/watch?v=BQPkRlbVFEs>`_

