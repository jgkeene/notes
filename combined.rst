

.. contents::
    :local:
    :depth: 6

Languages
##########

Python
***********

Shell
***********

SQL
***********

JS
***********




Tools
##########

Git
*****


Linux
*******

Commands
----------


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
--------


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
- There are three timestamps: **atime** (accessed), **mtime** (modified), **ctime** (changed ownership/permis


Ubuntu
-------
