Technical Notes
###############

.. contents::
    :local:
    :depth: 5

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

.. code-block:: bash

    pip3 install --user ./PAKAGE.tar.gz
    
Virtualenv 

.. code-block:: bash 

    # Install
    sudo apt install python-virtualenv

    # Create virtualenv directory
    virtualenv -p python3 ./myvenv 
    . ./myvenv/bin/activate 
    deactivate
    
Jupyter Notebook

.. code-block:: bash

    # Ensure that you have the latest pip
    sudo -H pip3 install --upgrade pip

    # Install Jupyter Notebook
    sudo -H pip3 install jupyter

Web scraping 

.. code-block:: text

    beautifulsoup 
    urllib2 
    lxml 
    requests 
    selenium 
    webdriver 

Managing project dependencies 

.. code-block:: bash

    pip freeze > requirements.txt 
    pip install -r requirements.txt 

Inspecting objects 

.. code-block:: python 
	
    # What object takes resposibility
    import inspect
    inspect.getmro(type(OBJECT))

    # Is one obj like another
    isinstance('foo', type(''))                        

    # Namespace of obj
    dir(OBJECT) 	

    # Address of obj
    id(OBJECT)

    # Class membership of obj 
    OBJECT.__class__

    # Docstring of obj
    OBJECT.__doc__ 

     # The assembly equivilant to your code  
    import codeop, dis
    dis.dis(codeop.compile_command('l = []; l += 1')

Debugging 

.. code-block:: python

    python -m pydb my_script.py

C & C++
=======

.. code-block:: bash

  sudo apt install build-essential      # c compiler
  sudo apt install lldb-3.6             # lldb
  sudo apt install valgrind             # valgrind
  sudo apt install lib64asan0           # address sanitizer
  sudo apt install ack-grep             # ack-grep
  sudo apt install splint               # splint

  # Pass arguments among your program and the debugger
  gdb --args

  # Dump backtrace for all threads (useful)
  thread apply all bt

  # Run program, and provide backtrace if it bombs
  gdb --batch --ex r --ex bt --ex q --args

Compiling commands

.. code-block:: bash

  # Src -> obj -> shared obj
  cc -shared -o libex29.so -fPIC libex29.c

  # Src -> binary
  cc -Wall -g -DNDEBUG ex29.c -ldl -o ex29

Install gcc manpages

.. code-block:: bash

  sudo apt install manpages-dev
  sudo apt install manpages-posix-dev
  sudo apt install glibc-doc

C degubbers

.. code-block:: bash

  # equalx
  sudo apt-add-repository -y ppa:q-quark/equalx
  sudo apt update
  sudo apt install equalx

  #lyx
  sudo apt-add-repository -y ppa:lyx-devel/release
  sudo apt update
  sudo apt install lyx


