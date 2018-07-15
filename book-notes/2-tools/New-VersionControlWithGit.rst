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


- Index stored in ``/.git/index``
- Stores the pathnames and blobs whenever you ``git add`` 

::

  git ls-files --stage          Lists contents of index

  git status                    List staged/unstaged changes
  git diff                      List unstaged changes
  git diff --cached             List staged changes

  git add                       Add to index
  git rm --cached               Remove from index
  git rm                        Remove from index and local filesystem
  git checkout HEAD -- FILE     Recover file



- Compute hash from a file ``git hash-object FILE``


6 - Commits
===========


::

  git show-branch --more=99999        List all relative commit names
  git rev-list --all                  List all absolute commit names (HASH)
  git rev-parse COMMIT-NAME           List the HASH for the commit name

  git log FILE                        Show logs for a file
  git log --follow FILE               Show logs for a file, following any renaming
  git log -Ssearch_string debian.rst  Search diffs of a file for specific string 

  git log master^^^..master           Show commit details for range of commits
  git log --stat master^^^..master    Show only file changes for range of commits

  git show master                     Show commit details for a single commit
  git show --stat master              Show file changes for a single commit
  git show master:debian.rst          Show file contents for a single commit 

7 - Branches
=============

::

  git branch --all                              Show simple branch info
  git show-branch --all                         Show detailed branch info

  git branch NEW-BRANCH STARTING-COMMIT         Create a branch at a specific commit
  git checkout NEW-BRANCH                       Switch to another branch

  git checkout -m NEW-BRANCH                    Switch to another branch and attempt to merge changes

  git checkout -d NEW-BRANCH                    Delete a branch

  git diff NEW-BRANCH master                    Show diff between branches
  git merge-base ORIGINAL-BRANCH NEW-BRANCH     Show which commit this branch came from

8 - Diffs
========================

9 - Merges 
========================

10 - Altering Commits
========================

11 - Stash & Reflog
========================

8 -
========================


