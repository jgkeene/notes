Debian 
########

.. contents::
    :local:
    :depth: 5

- Every file has a 4 digit **umask** that specifies rwx permissions and filetype
- Every file has a datastruct called an **inode** that stores permissions and timestamps
- There are three timestamps: **atime** (accessed), **mtime** (modified), **ctime** (changed ownership/permission)

Commands
========

rsync
----- 

You can use ``-aHAXSv`` for ``rsync`` to make backups

.. code-block:: bash

  rsync -aHAXSv --delete --info=progress3 --partial-dir=/home/azhee/Documents/.rsync-partial /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures

Others say all you need is ``-a`` and ``--delete``

.. code-block:: bash

  rsync -a /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures 

cp
-----

You can use ``-a`` with ``cp`` to make backups, worse performance than rsync

.. code-block:: bash

  cp -a /home/azhee/Pictures /media/azhee/backup/debian-backups/rsync/Pictures

tar
---

.. code-block:: bash

  # Compress
  tar -cvf DIR.tar DIR
  # List contents
  tar -tvf DIR.tar
  # Extract 
  tar -xvf DIR.tar


find
-----

``find . -size +1M``

``find . \
  -type f -not -perm 0600 -or \
  -type d -not -perm 0700``

find . \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)


# The + sign is faster and formats better than using the \ sign
find . -type f -exec cat '{}' \;
find . -type f -exec cat '{}' +

# Using print & xargs is equivalent to using exec
find . print | xargs cat 

# To protect against filenames with escape chars, use print0 & null when using xargs
find . -print0 | xargs -null cat


diff -u  oldfile newfile > patchfile
patch oldfile < patchfile


- stat
- fc
- umask
- help (bash's own interactive help) 







Docs
====
- `Docs <https://www.debian.org/doc/>`_
- `Wiki <https://wiki.debian.org/>`_
- `Manpages <https://manpages.debian.org/>`_

