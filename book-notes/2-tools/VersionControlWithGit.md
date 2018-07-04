`git push git@gist.github.com:f73a1676c101f3656bc2644e58fd5ac5`


Preface
===
- No notes.


Chapter 1 - Introduction
===
- General CVS overview. Git development history & features. No notes.


Chapter 2 - Installing Git
===
- Install Git - ``$ sudo apt-get install git-all``
- Important Git packages - `` git git-doc gitweb git-gui gitk git-email git-svn ``


Chapter 3 - Getting Started
===
##### Note: all examples in this chapter were done completely on the *local filesystem*
**_Help_**

- List all commands `git help --all`

**_Configuring the Commit Author_**
```bash
$ git config user.name "Jon Loeliger"
$ git config user.email "jdl@example.com"

# or set the environmental variables
export GIT_AUTHOR_NAME='Jon Loeliger'
export GIT_AUTHOR_EMAIL='jdl@example.com'

```
- `git log` - general info, commit ID#s
- `git show ID#` - more detailed info, specific commit ID#
- `git show-branch --more=10` - shows commits on current branch, up to 10
- `git diff ID#1 ID#2` - compare two revisions
- `git rm file` - remove
- `git mv file1 file2` - rename
- `git clone`
- Hierachry of configuration files (decreasing precedence)
    1. **Current Repository** - <i>`.git/config`</i> - repository-specific settings
        - manipulated by default, *highest presedence*
            ```
            $ git config user.name "Jesse Keene"
            $ git config user.email "jgkeene@gmail.com"
            ```
    2. **Home Directory** - `~/.gitconfig` - user-specific settings
        - manipulated with the `--global` option
            ```
            $ git config --global user.name "Jesse Keene"
            $ git config --global user.email "jgkeene@gmail.com"
            ```
    3. **Root Directory** - `/etc/gitconfig` - system-wide settings
        - manipulated with the `--system` option
- `git config -l` - list all settings found among *all* configuration files
- `--unset` - remove a setting
    ```
    $ git config --unset --global user.email
    ```
- Multiple configuration options & environment variables exist for the *same*
  purpose
    - ex: the editor used for commit messages follows these steps in order
    ```bash
        GIT_EDITOR  - environment variable
        core.editor - configuration option
        VISUAL      - environment variable
        EDITOR      - environment variable
        the vi command 
    ```
- Configuring an Alias 
    ```
    git config --global \
        alias.show-graph \
        'log --graph --abbrev-commit --pretty=oneline'
    ```

## Links
- [Official Documentation](https://www.git-scm.com/doc)
- [Official Downloads](https://www.git-scm.com/downloads)
- [Wikipedia - Git](https://en.wikipedia.org/wiki/Git)
- [Online `git` manpage](https://www.kernel.org/pub/software/scm/git/docs/)

## Discusion
- You can use local repos out of the box, as long as you never push.
- I learned how to setup git aliases.



Chapter 4 - Basic Git Concepts
===
Terms: `repository object store index blob tree commit tag`
- **repository** - A database containing all the info needed to retain and manage.
  a project. Repositories store a copy of *all files* and a copy of the *repository itself*.
- 2 <u>datastructures</u> (inside each repository):
  1. **object store** - The heart of the repository. It contains your original data files and all the log messages, author information, dates, and other infor- mation required to rebuild any version or branch of the project.Is copied during a clone operation.
  2. **index** - A snapshot of entire directory structure of the repository at some moment in time. You execute Git commands to stage changes in the index. Changes usually add, delete, or edit some file or set of files. The index records and retains those changes, keeping them safe until you are ready to commit them.
- 4 <u>types of objects</u> (in the *object store*):
  1. **Blob** - Store binary blob versions for each file.
  2. **Trees** - Store blob identifiers, path names, and file metadata for all files in a directory.
  3. **Commits** - Store commit metadata, each commit points to a *tree* object that captures a snapshot.
  4. **Tags** - Store a human-readable alias to a commit id.
  


