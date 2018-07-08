Debian 
########

From "Debian Manual"
===================
- Every file has an inode that stores it's attributes (user/group ownership, various timestamps)
- There are three timestamps: atime (accessed), mtime (modified), ctime (changed ownership/permission)
- They use this for ``rsync``

.. code-block:: bash

  rsync -aHAXSv ./source/ /dest

- They exclude files using ``-prune -or`` with ``find``

.. code-block:: bash

  find . \
    -type d -regex ".*/\.git" -prune -or
    -type d -regex ".*/\.idea" -prune -or
    -type f -size +10M -prune -or-print0
       
Nostarch
========
- 



Docs
====
- `Docs <https://www.debian.org/doc/>`_
- `Wiki <https://wiki.debian.org/>`_
- `Manpages <https://manpages.debian.org/>`_

