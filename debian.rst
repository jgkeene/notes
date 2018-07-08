Debian 
########

.. contents::
    :local:
    :depth: 5

From "Debian Manual"
===================
- Every file has an inode that stores it's attributes (user/group ownership, various timestamps)
- There are three timestamps: atime (accessed), mtime (modified), ctime (changed ownership/permission)
- They use `-aHAXSv` for ``rsync``

.. code-block:: bash

  rsync -aHAXSv ./source/ /dest

- They exclude files using ``-prune -or`` with ``find``

.. code-block:: bash

  find . \
    -type d -regex ".*/\.git" -prune -or
    -type d -regex ".*/\.idea" -prune -or
    -type f -size +10M -prune -or-print0

- Use `fc` to edit a long command in vim and then run it       

Nostarch
========
- 



Docs
====
- `Docs <https://www.debian.org/doc/>`_
- `Wiki <https://wiki.debian.org/>`_
- `Manpages <https://manpages.debian.org/>`_

