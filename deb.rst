Deb
#####

.. contents::
        :local:
        :depth: 5

1
====
- Every file has an *inode* that stores it's attributes (user/group ownership, various timestamps)
- There are three timestamps: atime (accessed), mtime (modified), ctime (changed ownership/permission)
- They use this for rsync:

.. code-block:: bash
        rsync -aHAXSv ./source/ /dest

- They use this for finding files

.. code-block:: bash
        find . \
                -type d -regex ".*/\.git" -prune -o
                -type d -regex ".*/\.idea" -prune -o
                -type f -size +10M -prune -o -print0
        




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

