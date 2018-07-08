TR
###############

.. contents::
    :local:
    :depth: 5


1
====
- Every kind of filesystem object (files, directories, devices, named-pipes) has a datastruct called an *inode* that stores the attributes (user/group ownership, various timestamps)
- There are three timestamps:
        - **atime**: accessed (`ls -lu`)
        - **mtime**: modified (`ls -l`)
        - **ctime**: changed owner/permission (`ls -lc`)
- Use the first bit of `ls` to tell if it's a normal, directory, symlink, character-device, block-device, named-pipe, or socket file
- Use `umask -p` or `umask -S` to



Setup
====

Thoughts: Dump & Process 
====

Actions: Review & Do
====

Projects: Review & Plan
====


