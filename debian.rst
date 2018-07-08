Debian 
########

.. contents::
    :local:
    :depth: 5

- Every file has a datastruct called an **inode** that stores permissions and timestamps
- There are three timestamps: **atime** (accessed), **mtime** (modified), **ctime** (changed ownership/permission)

Commands
========

Rsync
----- 

They use ``-aHAXSv`` for ``rsync``

.. code-block:: bash

  rsync -aHAXSv ./source/ /dest

They exclude files using ``-prune -or`` for ``find``

.. code-block:: bash

  find . \
    -type d -regex ".*/\.git" -prune -or
    -type d -regex ".*/\.idea" -prune -or
    -type f -size +10M -prune -print0



Docs
====
- `Docs <https://www.debian.org/doc/>`_
- `Wiki <https://wiki.debian.org/>`_
- `Manpages <https://manpages.debian.org/>`_

