Install pip

azhee@azhee:/media/azhee/backup$ sudo python3 ./get-pip.py 
[sudo] password for azhee: 
Collecting pip
  Downloading https://files.pythonhosted.org/packages/5f/25/e52d3f31441505a5f3af41213346e5b6c221c9e086a166f3703d2ddaf940/pip-18.0-py2.py3-none-any.whl (1.3MB)
    100% |████████████████████████████████| 1.3MB 16.5MB/s 
Collecting setuptools
  Downloading https://files.pythonhosted.org/packages/ff/f4/385715ccc461885f3cedf57a41ae3c12b5fec3f35cce4c8706b1a112a133/setuptools-40.0.0-py2.py3-none-any.whl (567kB)
    100% |████████████████████████████████| 573kB 16.2MB/s 
Collecting wheel
  Downloading https://files.pythonhosted.org/packages/81/30/e935244ca6165187ae8be876b6316ae201b71485538ffac1d718843025a9/wheel-0.31.1-py2.py3-none-any.whl (41kB)
    100% |████████████████████████████████| 51kB 19.9MB/s 
Installing collected packages: pip, setuptools, wheel
Successfully installed pip-18.0 setuptools-40.0.0 wheel-0.31.1


Install virtualenv

azhee@azhee:/media/azhee/backup$ pip3 install --user virtualenv
Collecting virtualenv
  Downloading https://files.pythonhosted.org/packages/b6/30/96a02b2287098b23b875bc8c2f58071c35d2efe84f747b64d523721dc2b5/virtualenv-16.0.0-py2.py3-none-any.whl (1.9MB)
    100% |████████████████████████████████| 1.9MB 2.1MB/s 
Installing collected packages: virtualenv
  The script virtualenv is installed in '/home/azhee/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed virtualenv-16.0.0


Other packages

Install pipenv

azhee@azhee:/media/azhee/backup$ pip3 install --user pipenv
Collecting pipenv
  Downloading https://files.pythonhosted.org/packages/eb/64/9b2747d54f2008ac3dfe86c0b1c8ec126042726fd8a540d5208d26732701/pipenv-2018.7.1-py3-none-any.whl (5.0MB)
    100% |████████████████████████████████| 5.0MB 3.2MB/s 
Requirement already satisfied: setuptools>=36.2.1 in /usr/local/lib/python3.5/dist-packages (from pipenv) (40.0.0)
Requirement already satisfied: virtualenv in /home/azhee/.local/lib/python3.5/site-packages (from pipenv) (16.0.0)
Collecting certifi (from pipenv)
  Downloading https://files.pythonhosted.org/packages/7c/e6/92ad559b7192d846975fc916b65f667c7b8c3a32bea7372340bfe9a15fa5/certifi-2018.4.16-py2.py3-none-any.whl (150kB)
    100% |████████████████████████████████| 153kB 3.9MB/s 
Collecting virtualenv-clone>=0.2.5 (from pipenv)
  Downloading https://files.pythonhosted.org/packages/6d/c2/dccb5ccf599e0c5d1eea6acbd058af7a71384f9740179db67a9182a24798/virtualenv_clone-0.3.0-py2.py3-none-any.whl
Requirement already satisfied: pip>=9.0.1 in /usr/local/lib/python3.5/dist-packages (from pipenv) (18.0)
Installing collected packages: certifi, virtualenv-clone, pipenv
  The script virtualenv-clone is installed in '/home/azhee/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The scripts pewtwo, pipenv and pipenv-resolver are installed in '/home/azhee/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.


Install pandoc (needed for sublime rst previewr)

azhee@azhee:/media/azhee/backup$ sudo apt install pandoc pandoc-citeproc
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
azhee@azhee:/media/azhee/backup$ clear

azhee@azhee:/media/azhee/backup$ sudo apt install pandoc pandoc-citeproc
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libbibutils2 libghc-pandoc-citeproc-data liblua5.1-0 libluajit-5.1-2 libluajit-5.1-common pandoc-data
Suggested packages:
  texlive-latex-recommended texlive-xetex texlive-luatex texlive-latex-extra wkhtmltopdf
The following NEW packages will be installed:
  libbibutils2 libghc-pandoc-citeproc-data liblua5.1-0 libluajit-5.1-2 libluajit-5.1-common pandoc pandoc-citeproc pandoc-data
