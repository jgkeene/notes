Debian Notes
############

.. contents::
    :local:
    :depth: 5
Docs
====

https://www.debian.org/doc/
https://wiki.debian.org/
http://forums.debian.net/
https://www.debian.org/doc/manuals/refcard/refcard
https://www.debian.org/doc/manuals/debian-handbook/
https://www.debian.org/doc/manuals/debian-reference/
https://www.debian.org/doc/manuals/debian-faq/index.en.htmlhv
https://manpages.debian.org/


https://www.debian.org/doc/user-manuals#quick-reference
https://www.debian.org/doc/#howtos
https://www.debian.org/doc/user-manuals

https://www.debian.org/doc/manuals/debian-faq/index.en.html

Rsync
------

.. code-block:: text

    mkdir ~/.rsync-partial
    
    rsync --verbose --recursive --dry-run --times --partial-dir=/home/azhee/.rsync-partial --info=progress2 SOURCE DEST
    rsync --verbose --recursive --times --partial-dir=/home/azhee/.rsync-partial --info=progress2 SOURCE DEST

Swap caps/ctrl keys
-------------------

Using only buit-ins `(source) <http://www.noah.org/wiki/CapsLock_Remap_Howto>`_

.. code-block:: text

    # For consoles
    sudo vim /etc/default/kebboard 
    # Add this line
    `XKBOPTIONS="ctrl:swapcaps"`
    # Update our new setting
    sudo dpkg-reconfigure -phigh console-setup

    # For X11
    vim ~/.bashrc
    # Add this line
    setxkbmap -layout us -option ctrl:nocaps
