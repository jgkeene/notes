

.. contents::
  :local:
  :depth: 6


Languages
##########


Python
***********

Pip ::

  # https://pip.pypa.io/en/stable/installing/
  wget https://bootstrap.pypa.io/get-pip.py
  sudo -H python3 ./get-pip.py

Installing Packages With Pip, Over The Internet:: 

  pip3 install --user PACKAGE

Installing Packages With Pip, From File Downloaded From `Pypi <https://pypi.org/>`_

.. code-block:: bash

  pip3 install --user ./PAKAGE.tar.gz

Virtualenv 

.. code-block:: bash 

  # Install
  sudo apt install python-virtualenv

  # Create virtualenv directory
  virtualenv -p python3 ./myvenv 
  . ./myvenv/bin/activate 
  deactivate


Jupyter Notebook

.. code-block:: bash

  # Ensure that you have the latest pip
  sudo -H pip3 install --upgrade pip

  # Install Jupyter Notebook
  sudo -H pip3 install jupyter


Web scraping 

.. code-block:: text

  beautifulsoup 
  urllib2 
  lxml 
  requests 
  selenium 
  webdriver 


Managing project dependencies 

.. code-block:: bash

  pip freeze > requirements.txt 
  pip install -r requirements.txt 


Inspecting objects 

.. code-block:: python 

  # What object takes resposibility
  import inspect
  inspect.getmro(type(OBJECT))

  # Is one obj like another
  isinstance('foo', type(''))                        

  # Namespace of obj
  dir(OBJECT)   

  # Address of obj
  id(OBJECT)

  # Class membership of obj 
  OBJECT.__class__

  # Docstring of obj
  OBJECT.__doc__ 

  # The assembly equivilant to your code  
  import codeop, dis
  dis.dis(codeop.compile_command('l = []; l += 1')

Debugging 

.. code-block:: python

  python -m pydb my_script.py



Shell
***********


SQL

***********

JS
***********

C/C++
*************

.. code-block:: bash

  sudo apt install build-essential      # c compiler
  sudo apt install lldb-3.6             # lldb
  sudo apt install valgrind             # valgrind
  sudo apt install lib64asan0           # address sanitizer
  sudo apt install ack-grep             # ack-grep
  sudo apt install splint               # splint

  # Pass arguments among your program and the debugger
  gdb --args

  # Dump backtrace for all threads (useful)
  thread apply all bt

  # Run program, and provide backtrace if it bombs
  gdb --batch --ex r --ex bt --ex q --args

Compiling commands

.. code-block:: bash

  # Src -> obj -> shared obj
  cc -shared -o libex29.so -fPIC libex29.c

  # Src -> binary
  cc -Wall -g -DNDEBUG ex29.c -ldl -o ex29

Install gcc manpages

.. code-block:: bash

  sudo apt install manpages-dev
  sudo apt install manpages-posix-dev
  sudo apt install glibc-doc

C degubbers

.. code-block:: bash

  # equalx
  sudo apt-add-repository -y ppa:q-quark/equalx
  sudo apt update
  sudo apt install equalx

  #lyx
  sudo apt-add-repository -y ppa:lyx-devel/release
  sudo apt update
  sudo apt install lyx




Tools
##########


Git
*****

Vim
****

Opening Files From Shell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  # Open in tabs
  vim -p FILE FILE FILE
  # Open in splits
  vim -O FILE FILE FILE


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



Linux
*******


Commands
=========


rsync
~~~~~

.. code-block:: bash11

  rsync --verbose --recursive --times --partial-dir=/home/azhee/.rsync-partial --info=progress2 SOURCE DEST


find
~~~~~

.. code-block:: bash

  find . -name "*.mp3" | grep -o '.*/' | sort | uniq
  find . -type f \( -name "*.py" -o -name "*.txt" \)

grep
~~~~~

.. code-block:: bash

  grep -n SEARCHTERM FILE


curl
~~~~~

.. code-block:: bash

  # Downlaod a file
  curl URL --output FILE
  # DownloadURL  multiple files matching a patterns
  curl URL 2> /dev/null |
  grep -iE '(FUCK|YOU)' |
  sed -E 's/^.*href="(.*)".*$/\1/' |
  while read line; do
  echo "http://www.whyprime.com/temp/destroy_all_software/"$line
  done

awk
~~~~

.. code-block:: bash

  # Print the nth word (awk treats whitespace as word delimeters)
  awk '{print $1}'



Viewing Manpages
~~~~~~~~~~~~~~~~~~

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


Monitor A Scheduled Crontab Job
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  watch -c -d -n 1 tail /var/log/syslog


Converting Files
~~~~~~~~~~~~~~~~~

.. code-block:: bash

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


View Files From A Clonezilla Backup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  # Extract into an image file
  sudo su
  cat sda2.ext4-ptcl-img.gz.* | gunzip -c | partclone.restore -s - -W -o./sda2.img



Debian
=======

rsync
~~~~~~

You can use ``-aHAXSv`` for ``rsync`` to make backups

.. code-block:: bash

  rsync -aHAXSv --delete --info=progress3 --partial-dir=/home/azhee/Documents/.rsync-partial /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures


Others say all you need is ``-a`` and ``--delete``

.. code-block:: bash

  rsync -a /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures 

cp
~~~~~~

You can use ``-a`` with ``cp`` to make backups, worse performance than rsync

.. code-block:: bash

  cp -a /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures


tar
~~~~~~

.. code-block:: bash

  # Compress
  tar -cvf DIR.tar DIR
  # List contents
  tar -tvf DIR.tar
  # Extract 
  tar -xvf DIR.tar


find
~~~~~~

.. code-block:: bash

  find . -size +1M
  find . \( -type f -not -perm 0600 \)-or  \( -type d -not -perm 0700 \)
  # The + sign is faster and formats better than using the \ sign
  find . -type f -exec cat '{}' \;
  find . -type f -exec cat '{}' +
  # Using print & xargs is equivalent to using exec
  find . print | xargs cat 
  # To protect against filenames with escape chars, use print0 & null when using xargs
  find . -print0 | xargs -null cat


misc
~~~~~~

.. code-block:: bash

  diff -u  oldfile newfile > patchfile 
  then patch oldfile < patchfile

  stat ?
  fc  ?
  umask ?
  help ? (interactive help)


- Every file has a 4 digit **umask** that specifies rwx permissions and filetype
- Every file has a datastruct called an **inode** that stores permissions and timestamps
- There are three timestamps: **atime** (accessed), **mtime** (modified), **ctime** (changed ownership/permission)


Ubuntu
==============


Keyboard Fixes
~~~~~~~~~~~~~~~~~~~

- Capslock `(source) <http://www.noah.org/wiki/CapsLock_Remap_Howto>`_ 
- Numlock `(source) <https://help.ubuntu.com/community/NumLock>`_ 
- Numlock `(source) <https://help.ubuntu.com/community/NumLock>`_


Setting Up SMB Shares
~~~~~~~~~~~~~~~~~~~

`(source) <http://www.configserverfirewall.com/ubuntu-linux/mount-samba-share-ubuntu-cifs/>`_

.. code-block:: bash

  sudo apt install cifs-utils
  # Manual mount via Nautilus
  nautilus --select smb://192.168.0.3/nfs
  # Results
  $ mount | grep gvfsd-fuse
  gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)

  # Automatic mount, via fstab
  mkdir /media/azhee/nfs
  sudo vim /etc/fstab
  //192.168.0.3/nfs  /media/azhee/nfs  cifs  rw,_netdev,username=0,password=0,users  0 0
  mount | grep cifs
  //192.168.0.3/nfs on /media/azhee/nfs type cifs (rw,nosuid,nodev,relatime,vers=default,cache=strict,username=0,domain=,uid=1000,forceuid,gid=1000,forcegid,addr=192.168.0.3,file_mode=0755,dir_mode=0755,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,echo_interval=60,actimeo=1,_netdev)


View and Save Dconf Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  # dump dconf settings
  dconf dump / >> ./dump.txt
  # restore dconf settings
  dconf load ./dump.txt


View Installed Software
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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



