Technical Notes
###############

.. contents::
    :local:
    :depth: 5

Ubuntu
======

Enable numlock on every boot, both ttys and X11 `(Ubuntu Help Wiki) <https://help.ubuntu.com/community/NumLock>`_

.. code-block:: bash

    # For ttys
    sudo vim /etc/rc.local
    
    # Add this loop
    for tty in /dev/tty[1-6]; do
      /usr/bin/setleds -D +num < $tty
    done
    
    # For X11
    sudo apt install numlockx
    sudo vim /usr/share/lightdm/lightdm.conf.d/50-unity-greeter.conf
    
    # Add this line
    greeter-setup-script=/usr/bin/numlockx on

Map caps-lock to ctrl

.. code-block:: bash

    gnome-tweak-tool
    
    # Typing>CtrlKeyPosition>"Caps lock as ctrl"
    # Typing>CapsLockKeyBehavior>"Disabled"

Clear crashlog

.. code-block:: bash
        
    sudo rm -f /var/crash/*

Disable wifi on boot `(AskUbuntu) <https://askubuntu.com/questions/964134/ubuntu-16-04-disable-internal-wifi-while-enabling-external-wifi-adapter/964196#964196>`_

.. code-block:: bash
        
    sudo vim /etc/network/interfaces

    # Add this line
    iface wlo1 inet manual

Fonts

.. code-block:: bash

    mkdir ~/.fonts
    # copy fonts into it
    fc-cache -fv

Sound equalization

.. code-block:: bash

    sudo apt-add-repository ppa:nilarimogard/webupd8
    sudo apt update
    sudo apt install pulseaudio-equalizer

Copy text from terminal

.. code-block:: bash

    xclip -sel clip < ~/.ssh/id_rsa.pub

HDD recovery tools

.. code-block:: text

    gddrescue
    testdisk
    photorec
    kpartx

A HDD recovery procedure for failed drive

.. code-block:: bash

    # Make a backup image of HDD
    gddrescue

    # Make a copy of backup image
    testdisk
    
    # Try to recover files from image copy

Making Ubuntu Backups
---------------------

Use `Aptik <http://www.teejeetech.in/p/aptik.html>`_ to backup software installed via apt, ppa, and .deb

.. code-block:: bash

    sudo apt-add-repository -y ppa:teejee2008/ppa
    sudo apt update
    sudo apt install aptik

Use `Timeshift <http://www.teejeetech.in/p/timeshift.html>`_ to backup system files

.. code-block:: bash

    sudo apt-add-repository -y ppa:teejee2008/ppa
    sudo apt update
    sudo apt install timeshift

Use `BackInTime <https://github.com/bit-team/backintime>`_ to backup user files

.. code-block:: bash

    sudo apt-add-repository -y ppa:bit-team/stable
    sudo apt update
    sudo apt install backintime-qt4
    
View Files From A Clonezilla Backup
-----------------------------------

.. code-block:: bash

    # Extract into an image file
    cat sda2.ext4-ptcl-img.gz.aa | gunzip -c | partclone.restore -s - -W -O ./sdb2.ext4.img

    # Mount the image file and browse files
    
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

Bash
====

Find directories containing specific file extension

.. code-block:: bash

    find . -name "*.mp3" | grep -o '.*/' | sort | uniq

Find files, using multiple keywords

.. code-block:: bash

    find . -type f \( -name "*.py" -o -name "*.txt" \)

Find matching files, line numbers, and highlight

.. code-block:: bash

    # Search through a single file
    grep -n SEARCHTERM FILE

    # Search through multiple files, recursively
    grep -r -n SEARCHTERM ./*

Run process in background

.. code-block:: bash

    PROGRAM > /dev/null &

Tarball (tar & gzip) a DIRECTORY

.. code-block:: bash

    tar cvzf OUT.tar.gz DIRECTORY

Customize grub bootloader

.. code-block:: bash

    sudo vim /etc/default/grub
    sudo update-grub

Customize grub bootloader through GUI

.. code-block:: bash

    sudo apt-add-repository -y ppa:danielrichter2007/grub-customizer

Copy files

.. code-block:: bash

    rsync -avhr --no-compress --progress

Create application shortcut on desktop:

.. code-block:: bash

    cp /usr/share/applications/APPLICATION.desktop ~/Desktop
    chmod +x ~/Desktop/APPLICATION.desktop

Batch rename files

.. code-block:: bash

    # Numbering files (appended number)
    for i in *.png; do
        mv $i ${i/.png/-0}
    done

    # Numbering files (prepended number)
    for i in {1..9}; do
        mv file_$i `printf file_0$i`
    done

Securely delete files (similar programs do the same: srm, sfill, sswap, sdmem)

.. code-block:: bash

    srm -rvl ./*.html*

Use cronjobs

.. code-block:: bash

    # Schedule a job to run
    crontab -e

    # Monitor the job
    watch -c -d -n 1 tail /var/log/syslog

Downlaod a file

.. code-block:: bash

    curl https://raw.githubusercontent.com/garybernhardt/dotfiles/master/.vimrc --output FILE

Download multiple files matching a patterns

.. code-block:: bash

    curl http://www.whyprime.com/temp/destroy_all_software/ 2> /dev/null |
    grep -iE '(shell|bash|unix)' |
    sed -E 's/^.*href="(.*)".*$/\1/' |
    while read line; do
        echo "http://www.whyprime.com/temp/destroy_all_software/"$line
    done

Mirror an entire website

.. code-block:: bash

    wget \
      --user-agent="Mozilla/4.5" \
      --mirror \
      --convert-links \
      --adjust-extension \
      --page-requisites \
      --no-parent http://whatonearthishappening.com/podcast/

Print the nth word (awk treats whitespace as word delimeters)

.. code-block:: bash

    apt list --installed |
    awk '{print $1}'

Convert files

.. code-block:: bash

    # wav to mp3
    soundconverter
    
    # image to html - https://bitbucket.org/blais/curato
    curator
    
    # ppt to pdf
    soffice --headless --convert-to pdf in.ppt
    
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
    
Verify MD5 Checksums
--------------------
    
Download checksum file (MD5SUMS), and compare automatically

.. code-block:: bash

    md5sum --check ./MD5SUMS

Generate the MD5 checksum for your file, and compare it manually

.. code-block:: bash

    $ md5sum ./ubuntu-18.04-desktop-amd64.iso
    129292a182136a35e1f89c586dbac2e2  ./ubuntu-18.04-desktop-amd64.iso

    
Samba Windows Shares
--------------------

Install CIFS VFS (http://www.configserverfirewall.com/ubuntu-linux/mount-samba-share-ubuntu-cifs/)

.. code-block:: bash

    sudo apt update
    sudo apt install cifs-utils

Manual mount via Nautilus

.. code-block:: bash

    nautilus --select smb://192.168.0.3/nfs

.. code-block:: bash

    # Results
    mount | grep gvfsd-fuse
    
.. code-block:: text

    gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)

Automatic mount, via fstab

.. code-block:: bash

    # Make mount-point
    mkdir /media/azhee/nfs
    # Edit fstab
    sudo vim /etc/fstab
    # Add this line
    //192.168.0.3/nfs  /media/azhee/nfs  cifs  rw,_netdev,username=0,password=0,users  0 0 

Results:

.. code-block:: bash

    mount | grep cifs

.. code-block:: text

    //192.168.0.3/nfs on /media/azhee/nfs type cifs (rw,nosuid,nodev,relatime,vers=default,cache=strict,username=0,domain=,uid=1000,forceuid,gid=1000,forcegid,addr=192.168.0.3,file_mode=0755,dir_mode=0755,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,echo_interval=60,actimeo=1,_netdev)

Python
======

Pip

.. code-block:: bash
    # https://pip.pypa.io/en/stable/installing/
    wget https://bootstrap.pypa.io/get-pip.py
    sudo -H python3 ./get-pip.py
    
Installing Packages With Pip, Over The Internet

.. code-block:: bash

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

C & C++
=======

.. code-block:: bash

    sudo apt install build-essential  		# c compiler
    sudo apt install lldb-3.6         		# lldb
    sudo apt install valgrind         		# valgrind
    sudo apt install lib64asan0       		# address sanitizer
    sudo apt install ack-grep         		# ack-grep
    sudo apt install splint           		# splint
    
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

    daw              		" Deleteword, better than 'dw'
    I                		" Begin of line, better than '0i'
    yiw              		" Copy word you're in
    mm -> `m         		" Mark cursor pos. as 'm' -> goto mark 'm'
    
    ctrl-w h        		" Move split left
    ctrl-w l       		" Move split right
    
    bo sp  			" Split horizontally across all windows
    
    z <cr> 			" Bring cursor position and screen to top of window
    
    z-R                 	" Open all folds
    z-M                     	" Close all folds
    
    g;                		" Goto prev edit position
    g,                		" Goto next edit position
    changes          		" List all edit positions
    
    =                 		" Auto-indent selected lines
    gg -> =G        		" Auto-indent all lines
    
    ctrl-pgUp          		" Goto next tab
    ctrl-pgDown        		" Goto prev tab
    
    :set list     		" Show hidden chars (tabs, spaces, etc..)
    :set nolist  		" Hide hidden chars (tabs, spaces, etc..)
    
    :set colorcolumn=79     	" Draw vertical column
    
    :set colorscheme? 		" Check a setting 
    
    %s/^M$//g               	" Remove ^M chars (to get ^M in vim, type c-V -> c-M)
    
    qd                  	" Start recording macro to register d (possible registers are [a-z])
    q                   	" Stop recording macro
    @d                  	" Execute your macro
    @@                  	" Execute your macro again
    '<,'>normal @d      	" Execute your macro on a visual selection
    
    dt<     			" Delete till a char (ex: '<')
    
    =                   	" Auto-indent selected lines
    gg =G               	" Auto-indent all lines
    
    tabedit FILE 		" Open file into a new-tab
    
    yO -> (paste)     		" Paste and preserve formatting
    
    '{' & '}'           	" Jump through paragraphs
    '(' & ')'           	" Jump through sentences
    %                   	" Jump between braces/parens/etc
    
    g/^$/d                 	" Delete empty lines in insert mode
    '<,'>g/^$/d            	" Delete empty lines in visual mode

    :/\s\+$/     		" Hilight whitespace chars

    :set ff=unix     		" Convert a Windows file into a unix file

Low-level
=========

.. code-block:: bash

    stdout | pacat 					# https://www.youtube.com/watch?v=GtQdIYUtAHgs
    pacat /dev/urandom > padsp
    strace 						# See the system calls made by an program
    hopper   						# Disassembler
    xxd -s 0x7f0000 -g 1 mbp101_b02.rom | head -15  	# Hex viewer
    binwalk -E [filename]        			# File etropy viewer
    strings -n 4 -t x FILE				# Find string in a binary file
    zmap						# Nmap on steroids

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

reStructuredText
================

Examples:

- `Wikipedia <https://en.wikipedia.org/wiki/ReStructuredText>`_
- `Cheatsheet <https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst>`_
- `Official Quickstart Guide <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_
- `A README.rst on github <https://github.com/aol/moloch/blob/master/README.rst>`_

Atom
====

Install
-------

https://atom.io/

Install Packages
----------------

.. code-block:: bash

    apm install https://github.com/travs/markdown-pdf.git

Docs
----

https://flight-manual.atom.io/
