New Version Control With Git
#############################

.. contents::
    :local:
    :depth: 5


4 - Git Objects and Index
==========================

- Objects stored in ``/.git/objects/[2-digit-hex]/[38-digit-hex]``
- Make a *blob* object with ``git add FILE``
- Make a *tree* object with ``git write-tree``
- Make a *commit* object with ``echo -n "Commit message...\n" | git commit-tree TREE-HASH``
- Make a *tag* object with ``git tag -m "Tag version 1.0" v1.0 COMMIT-HASH``


::

  find .git/objects/ -type f -print | tr '/' ' ' | awk '{print $3 $4}' | while read line; do echo -e "\033[35m"; git cat-file -t $line; echo -e "\033\0m" ; echo -e "\033[33m"$line"\033[0m"; git cat-file -p $line; echo; done

  git cat-file -t HASH
  git cat-file -p HASH


- Index stored at ``.../.git/index``

::

  git status                  
  git ls-files --stage
  git diff --cached

  git add                       Add to index
  git rm --cached               Remove from index
  git rm                        Remove from index and local filesystem
  git checkout HEAD -- FILE     Recover file



- Compute hash from a file ``git hash-object FILE``
- View file history ``git log FILE`` and ``git log --follow FILE`` when the filename was changed
