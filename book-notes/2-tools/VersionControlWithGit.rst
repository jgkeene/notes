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
- General CVS overview. Git development history & features. No notes.

Chapter 2 - Installing Git
==============================
- Install Git ``sudo apt-get install git-all``
- Important Git packages ``git git-doc gitweb git-gui gitk git-email git-svn``

Chapter 3 - Getting Started
==============================
- List all commands ``git help --al1``

Configuring the Commit Author

.. code-block:: bash
  
  git config user.name "Jon Loeliger"
  git config user.email "jdl@example.com"


Set the environmental variables

.. code-block:: bash
  
  export GIT_AUTHOR_NAME='Jon Loeliger'
  export GIT_AUTHOR_EMAIL='jdl@example.com'


- `git log` - general info, commit ID#s
- `git show ID#` - more detailed info, specific commit ID#
- `git show-branch --more=10` - shows commits on current branch, up to 10
- `git diff ID#1 ID#2` - compare two revisions
- `git rm file` - remove
- `git mv file1 file2` - rename
- `git clone`


- Config file hierarchy
  1. Current Repository `.git/config` - repository-specific settings
    - manipulated by default, *highest presedence*
      - ``git config user.name "Jesse Keene"``
      - ``git config user.email "jgkeene@gmail.com"``
  2. Home Directory `~/.gitconfig` - user-specific settings
    - manipulated with the ``--global`` option
      - ``git config --global user.name "Jesse Keene"``
      - ``git config --global user.email "jgkeene@gmail.com"``
  3. Root Directory - `/etc/gitconfig` - system-wide settings
    - manipulated with the `--system` option


- `git config -l` - list all settings found among *all* configuration files
- `--unset` - remove a setting :: git config --unset --global user.email


Multiple configuration options & environment variables exist for the *same*
purpose

ex: the editor used for commit messages follows these steps in order

.. code-block:: bash

  GIT_EDITOR  - environment variable
  core.editor - configuration option
  VISUAL      - environment variable
  EDITOR      - environment variable


Configuring an Alias 

.. code-block:: bash

  git config --global \
    alias.show-graph \
    'log --graph --abbrev-commit --pretty=oneline'

Links
=================
- `Docs <https://www.git-scm.com/doc>`_
- https://www.git-scm.com/downloads
- https://en.wikipedia.org/wiki/Git
- https://www.kernel.org/pub/software/scm/git/docs/

Discusion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- You can use local repos out of the box, as long as you never push.
- I learned how to setup git aliases.



Chapter 4 - Basic Git Concepts
===================================

Terms ``repository object store index blob tree commit tag``

repository
  A database containing all the info needed to retain and manage a project. Repositories store a copy of *all files* and a copy of the *repository itself*.

- Two types of datastructs inside every repo, *object store* and *index.

object store
  The heart of the repository. It contains your original data files and all the log messages, author information, dates, and other information required to rebuild any version or branch of the project. Is copied during a clone operation.

index
  A snapshot of entire directory structure of the repository at some moment in time. You execute Git commands to stage changes in the index. Changes usually add, delete, or edit some file or set of files. The index records and retains those changes, keeping them safe until you are ready to commit them.


- Four types of objects, in the object store: *blob*, *Blob*, *Tree*, *Commit*, *Tag*

Blob 
  Store binary blob versions for each file.

Trees
  Store blob identifiers, path names, and file metadata for all files in a directory.

Commits 
  Store commit metadata, each commit points to a tree object that captures a snapshot.

Tags 
  Store a human-readable alias to a commit id.
 



Term
  It's definition


