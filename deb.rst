Deb
#####

1
====
- Every file has an inode that stores it's attributes (user/group ownership, various timestamps)
- There are three timestamps: atime (accessed), mtime (modified), ctime (changed ownership/permission)
- They use this for `rsync`

.. code-block:: bash

  rsync -aHAXSv ./source/ /dest

- They use this for `find`

.. code-block:: bash

  find . \
    -type d -regex ".*/\.git" -prune -o
    -type d -regex ".*/\.idea" -prune -o
    -type f -size +10M -prune -o -print0
        



