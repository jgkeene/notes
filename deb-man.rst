TR
###############

.. contents::
    :local:
    :depth: 5


1
====
- Everything is a file: file-files, directory-files, device-files, named-pipe-files
- Every file has a datastruct called an *inode* that stores it's attributes (user/group ownership, various timestamps)
- There are three timestamps:
        - **atime**: accessed (`ls -lu`)
        - **mtime**: modified (`ls -l`)
        - **ctime**: changed owner/permission (`ls -lc`)
- The first bit of `ls` tells if the file is a symlink, character-device, block-device, named-pipe, or socket-file

.. code-block:: bash
    
        rsync -aHAXSv ./source/ /etst

.. code-block:: ba 

        find . \
                -type d -regex ".*/\.git" -prune -o
                -type d -regex ".*/\.idea" -prune -o
                -type f -size +10M -prune -o -print0
        

Test
====
- ``echo 123 \ 
123123123 \ 
12312312312``



