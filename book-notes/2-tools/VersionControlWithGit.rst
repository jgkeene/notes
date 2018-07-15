Version Control With Git
#########################

.. contents::
    :local:
    :depth: 5


Preface
=============================
- No notes.

Chapter 1 - Introduction
==============================
- CVS overview. 

Chapter 2 - Installing Git
==============================
Install Git ::

  sudo apt install git-all


Other git packages ::

  git git-doc gitweb git-gui gitk git-email git-svn


Chapter 3 - Getting Started
==============================
Configuring the Commit Author

.. code-block:: bash
  
  git config user.name "Jon Loeliger"
  git config user.email "jdl@example.com"


Set the environmental variables

.. code-block:: bash
  
  export GIT_AUTHOR_NAME='Jon Loeliger'
  export GIT_AUTHOR_EMAIL='jdl@example.com'



- Config file hierarchy

  - 1. Config in current repo (default) ``.git/config`` - repository-specific settings 
  
  - 2. Home Directory ``--global`` ``~/.gitconfig`` - user-specific settings
  
  - 3. Root Directory - ``--system`` ``/etc/gitconfig`` - system-wide settings


- ``git config -l`` - list all settings found among *all* configuration files
- ``--unset`` - remove a setting :: git config --unset --global user.email


- Multiple configuration options & environment variables exist for the *same* purpose


- For example, each of these controls the editor used for commit messages ::

  core.editor - configuration option
  GIT_EDITOR  - environment variable
  VISUAL      - environment variable
  EDITOR      - environment variable


Configuring an Alias ::

  git config --global \ alias.show-graph \ 'log --graph --abbrev-commit --pretty=oneline'


Notes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- You can use local repos out of the box, as long as you never push.
- Using commit IDs to view history::

  git log                             shows commit IDs
  git show $ID                        show commit details by commit ID
  git diff $ID1 $ID2                  compare two commits



Chapter 4 - Basic Git Concepts
===================================

repository
  A database containing all the info needed to retain and manage a project. Repositories store a copy of *all files* and a copy of the *repository itself*.


There are two types of datastructs inside every repo: *object store* and *index.


object store
  The heart of the repository. It contains your original data files and all the log messages, author information, dates, and other information required to rebuild any version or branch of the project. Is copied during a clone operation.

index
  A snapshot of entire directory structure of the repository at some moment in time. You execute Git commands to stage changes in the index. Changes usually add, delete, or edit some file or set of files. The index records and retains those changes, keeping them safe until you are ready to commit them.


There are four types of objects, in the object store: *blob*, *Blob*, *Tree*, *Commit*, *Tag*


Blob 
  Store binary blob versions for each file.

Trees
  Store blob identifiers, path names, and file metadata for all files in a directory.

Commits 
  Store commit metadata, each commit points to a tree object that captures a snapshot.

Tags 
  Store a human-readable alias to a commit id.



Temp Notes
==========
- `Hyperlinked manpages <https://git.github.io/htmldocs/>`_

Show all settings and config files ::

  # ~/.gitconfig
  git config --global --list --show-origin
  # $REPO/.git/config
  git config --local --list --show-origin


View current variables and env settings

::

  git var -l

