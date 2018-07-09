Misc
####

.. contents::
  :local:
  :depth: 5


Linux Commands
========

rsync
-----

.. code-block:: bash11

  rsync --verbose --recursive --times --partial-dir=/home/azhee/.rsync-partial --info=progress2 SOURCE DEST


findgg/u
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

Viewing Manpages
-----------------

.. code-block:: bash

# yelp - browse and jump through manpage links
yelp man:grep
# groff - generate html manpage with groff, open with browser **(best for printing)**
sudo apt install groff
man --html=google-chrome-stable SOME_APPLICATION
# chrome 
sudo apt install txt2html
man SOME_APPLICATION | txt2html - | google-chrome-stable "data:text/html;base64,$(base64)"
#  lynx
sudo apt install man2html
zcat $(man --path 1 grep) | man2html -l | lynx -stdin
# w3m 
zcat $(man --path 1 grep) | man2html -l | w3m -T text/html

View Files From A Clonezilla Backup
-----------------------------------

.. code-block:: bash

# Extract into an image file
sudo su
cat sda2.ext4-ptcl-img.gz.* | gunzip -c | partclone.restore -s - -W -o./sda2.img


Monitor a scheduled crontab job
-------------------------------

.. code-block:: bash

watch -c -d -n 1 tail /var/log/syslog


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

Misc
~~~~~~~~~~~

Low-level things 

.. code-block:: bash

stdout | pacat          # https://www.youtube.com/watch?v=GtQdIYUtAHgs
pacat /dev/urandom > padsp
strace            # See the system calls made by an program
hopper              # Disassembler
xxd -s 0x7f0000 -g 1 mbp101_b02.rom | head -15    # Hex viewer
binwalk -E [filename]             # File etropy viewer
strings -n 4 -t x FILE        # Find string in a binary file
zmap            # Nmap on steroids

Spoof interface

.. code-block:: bash

# Via command line
ip link show interface
ip link set dev interface down
ip link set dev interface address XX:XX:XX:XX:XX:XX
ip link set dev interface up
#Via GUI
macchanger






