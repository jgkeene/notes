

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

Ubuntu
-------
