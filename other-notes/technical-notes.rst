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


Vim
===

Opening files from shell

.. code-block:: bash

    # Open in tabs
    vim -p FILE FILE FILE
    
    # Open in splits
    vim -O FILE FILE FILE

Important commands

.. code-block:: text

    daw              		" Deleteword, better than 'dw'
    I                		" Begin of line, better than '0i'
    yiw              		" Copy word you're in
    mm -> `m         		" Mark cursor pos. as 'm' -> goto mark 'm'
    
    ctrl-w h        		" Move split left
    ctrl-w l       		" Move split right
    
    bo sp  			" Split horizontally across all windows
    
    z <cr> 			" Bring cursor position and screen to top of window
    
    z-R                 	" Open all folds
    z-M                     	" Close all folds
    
    g;                		" Goto prev edit position
    g,                		" Goto next edit position
    changes          		" List all edit positions
    
    =                 		" Auto-indent selected lines
    gg -> =G        		" Auto-indent all lines
    
    ctrl-pgUp          		" Goto next tab
    ctrl-pgDown        		" Goto prev tab
    
    :set list     		" Show hidden chars (tabs, spaces, etc..)
    :set nolist  		" Hide hidden chars (tabs, spaces, etc..)
    
    :set colorcolumn=79     	" Draw vertical column
    
    :set colorscheme? 		" Check a setting 
    
    %s/^M$//g               	" Remove ^M chars (to get ^M in vim, type c-V -> c-M)
    
    qd                  	" Start recording macro to register d (possible registers are [a-z])
    q                   	" Stop recording macro
    @d                  	" Execute your macro
    @@                  	" Execute your macro again
    '<,'>normal @d      	" Execute your macro on a visual selection
    
    dt<     			" Delete till a char (ex: '<')
    
    =                   	" Auto-indent selected lines
    gg =G               	" Auto-indent all lines
    
    tabedit FILE 		" Open file into a new-tab
    
    yO -> (paste)     		" Paste and preserve formatting
    
    '{' & '}'           	" Jump through paragraphs
    '(' & ')'           	" Jump through sentences
    %                   	" Jump between braces/parens/etc
    
    g/^$/d                 	" Delete empty lines in insert mode
    '<,'>g/^$/d            	" Delete empty lines in visual mode

    :/\s\+$/     		" Hilight whitespace chars

    :set ff=unix     		" Convert a Windows file into a unix file

