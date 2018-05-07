# Chapter 2 - Properly Installing Python
- Ubuntu ships Python3 now [Ubuntu's Python Page](https://wiki.ubuntu.com/Python)
- If you're code is python2, you must include shebang in your scripts: `!#/usr/bin/env python2`

## Setuptools and Pip
- Don't use ubuntu package manager, get the latest version of pip [get-pip.py](https://bootstrap.pypa.io/get-pip.py)
- `wget https://bootstrap.pypa.io/get-pip.py`
- `sudo python3 get-pip.py`
- This will also install **setuptools** with **easy_install** bundled
- Pip is a superior version of easy_install, use pip
- See [“pip vs easy_install”](https://packaging.python.org/discussions/pip-vs-easy-install/?highlight=easy_install) and the [Python Packaging User Guide](https://packaging.python.org), which should your first reference for packaging questions

## C Development Tools
- `apt-get update --fix-missing`
- `sudo apt-get install python3-dev`
- Then, you can just `pip install --user <somepkg>` and you'll be able to build build tools that must be C compiled

## Virtualenv
- [virtualenv](https://pypi.python.org/pypi/virtualenv)
- `sudo apt-get install python-virtualenv` 
- `pip3 install --user virtualenv`
- Then, once you are in a virtual environment, you can always use the command pip, whether you are working with Python 2 or Python 3, so that is what we will do in the rest of this guide

- **Add libraries to the virtual env**
- Once  you  have  activated  the  virtual  environment,  the  first  pip  executable  in  your path  will  be  the  one  located  in  the  v3 folder, it will  install libraries into the following directory: `my-venv/lib/python3.4/site-packages/`
- `pip freeze > requirements.txt` when packaging for others
- `pip install -r requirements.txt` when installing from others
- To set dependencies when distributing a library, it is better to use the `install_requires`  keyword argument to the 	setup()` function in a `setup.py` file
- **Deactivate the virtual env**


# Chapter 3 - Your Development Environment

- [https://www.python.org/dev/peps/pep-0008/](PEP 8)

```
set textwidth=79  " lines longer than 79 columns will be broken
set shiftwidth=4  " >> & << indents 4 spaces
set tabstop=4     " a hard TAB displays as 4 columns
set expandtab     " insert spaces when hitting TABs
set softtabstop=4 " insert/delete 4 spaces when hitting a TAB/BACKSPACE
set shiftround    " round indent to multiple of 'shiftwidth'
set autoindent    " align the new line indent with the previous line
```

- [python.vim](http://bit.ly/python-vim) improvements over  the  syntax  file  included  in  Vim  6.1
- [SuperTab](http://bit.ly/supertab-vim) makescode completion more convenient by using the Tab key 
indent handles indentation settings for Python source files
- [indent](http://bit.ly/indent-vim)
- [vim-flake8] (https://github.com/nvie/vim-flake8)
- [PEP8] (http://pypi.python.org/pypi/pep8/)
- [Pyflakes] (http://pypi.python.org/pypi/pyflakes/)
- [syntastic] (https://github.com/scrooloose/syntastic)

```
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*
let g:syntastic_auto_loc_list=1
let g:syntastic_loc_list_heighht=5
```

- [Python-mode](https://github.com/klen/python-mode) lets you search through Python documentation and run Python code
- [IPython](http://ipython.org/)
- [BPython](http://bpython-interpreter.org/)

## Virtual Environments 

- You can't move a virtualenv dir once it's created, it's got relative links that'll break
- Specify the python version with `--python`
- Use the `<virtualenv-name>/bin/activate` script to set the PATH

```
cd my-project-folder
virtualenv --python python3 v3
source v3/bin/activate
```
- `deactivate` to end session
- [virtualenv docs](http://bit.ly/virtualenv-guide)
- [official virtualenv docs](https://virtualenv.pypa.io/en/latest/userguide.html)
- [official python packing guide](https://packaging.python.org)
- [Docker]( https://www.docker.com/) 
- [Docker docs](https://docs.docker.com/) 

# Chapter 4 - Write Great Code

- To access dictionary elements: Use `x **in** d` not `d.**has_key**`
- To manipulate list items: Use `**list comprehensions**` 
- To count/itterate list items: Use `**enumerate()**`
- If you know a list's length, you can give names to each item with `**unparing**`

```
filename, ext = "my_photo.orig.png".rsplit(".", 1)
print(filename, "is a", ext, "file.")
```

- Use `**unpacking to swap variables**`
```
a, b = b, a
a, (b, c) = 1, (2, 3)
a, *rest = [1, 2, 3] 		# a = 1, rest = [2, 3]
a, *middle, c = [1, 2, 3, 4] 	# a = 1, middle = [2, 3], c = 4
```
- To assign something while `**unpacking**~, and toss away the variable: use `**__**`
```
filename = 'foobar.txt'
basename, __, ext = filename.rpartition('.')
```
- To creat strings: Use `**str.join()**` on an empty string

```
letters = ['s', 'p', 'a', 'm']
word = ''.join(letters)
print(word) 			# spam
```

- Namespace Tools: dir(), globals(), and locals() 
- dir(object) returns a list of attributes that are accessible via the object
- globals() returns a dictionary of the attributes currently in the global name‐ space, along with their values.
- locals() returns a dictionary of the attributes in the current local namespace (e.g., within a function), along with their values.  

```bash
# NOTE: Always `import` things the following way.
        Unless it's a package that's deeply nested, in that case use `as` `very.deep.module as mod`
```
- To import: Use `import <modu>` then access functions explicitly using dot notation `modu.func()
- Modules lookup: local dir > pythonpath
- Packages: the top-lvl dir with an __init__.py is the "root package", it's modules in the package are imported

```
my_pack/
  modu.py
  __init__.py


. . . 
import my_pack.modu
```
- python looks for an __init__.py in this dir , executes all it's statements , vars, funcs, and classes avail to global ns


## OOP
http://bit.ly/functional-programming-python
- You don't have to use OOP in python
- Sometimes you just have to maintain state (webapps)
- State is maintained through class objects.
- This state is prone to **race conditions**, the difference in state between the world, vs a class obj
- They recommend using ***custom classes*** to seperate ***pure funcs*** from stateful funcs
- Pure funcs are, easier to test, easier to decorate, 


- Decorator - a func or class meth that ***wraps*** another func
- The decoratED funcor replaces the decoratING funct
Because functions are first-class objects in Python, this can

k
- Dynamic Typing


- Mutable and Immutable Types


- Testing


- Documentation


- Logging


## Terms
- race condition: static information about the world, is prone to race conditions, a term used to describe the situation where, at some point between the initialization of the state of an object (usually done with the Class.__init__() method in Python) and the actual use of the object state through one of its methods, the state of the world has changed.  For example, a request may load an item in memory and later mark it as added to a
- implicit context: fof a func, is madu up of, global vars & anything accessed from inside the func
- side effects: the changes that a func makes to it's implicit context (save/delete global variables for ex.)


## Notes
- Print like this from now on: `print('hear is a variable:{} and anothervariable:{} and yetanothervariable:{}'.format(x, y, z))`

# Chapter 5 - Read Great Code
# Chapter 7 - User Interaction









## Web Frameworks

- Web frameworks consists of *libraries* and *main handler*, utilities to handle:
    - URL Routing              - invokes specific Python code for HTTP requests
    - Request/Response Objects - encapsulates data sent
    - Template Engine          - seperates Python code (backend) from frontend
    - Development Web Server   - a local dev webserver, for rapid development, automatically reloads code when files are updated
- [**Django**](https://www.djangoproject.com/)
    - Batteries included framework
    - Good for content-oriented sites
    - DB-backed web apps quickly
    - https://www.djangoproject.com/
    - [extensions](https://djangopackages.org/)
- [**Flask**](http://flask.pocoo.org/)
    - Microframework
    - Good for smaller apps
    - Provides only the most used shit like URL routing, request and response objects, and templates
    - [extensions](http://flask.pocoo.org/extensions/)

## Web Template Engines

- Fills *static* content (from template), with *dynamic* content (generated by app)
- WSGI apps respond to HTTP requests, serve content in HTML
- [**Jinja2**](http://jinga.pocoo.org/)
    - default engine in Django & Flask
- [**Chameleon**](https://chameleon.readthedocs.io/en/latest/)
- [**Mako**](http://www.makotemplates.org/)
    - default engine in Pyramid, Speed focused

## Web Deployment
- Local server
    1. **WSGI Servers**
        - minimal, python-only webserver
        - [Gunicorn (recommended)](http://gunicorn.org/)
        - [Waitress](https://waitress.readthedocs.io/)
    2. **Web Servers**
        - resource heavy webserver
        - [Nginx (recommended)](http://nginx.org/)
            - high performance, simple, highly compatible
        - Apache
- Remote server
    1. **PaaS**
        - offsite, cloud hosted
        - cloud hosted
        - [Heroku (recommended)](http://www.heroku.com/python) [1](https://devcenter.heroku.com/categories/python) [2](https://devcenter.heroku.com/articles/getting-started-with-python#introduction)
        - Gondor

### Terms

- **WSGI** - Web - Server - Gateway - Interface
    - WSGI is not a server, a python module, a framework, or an API
    - WSGI is just an interface specification by which server and application communicate. Both server and application interface sides are specified in the PEP 3333. If an application (or framework or toolkit) is written to the WSGI spec then it will run on any server written to that spec.
    applications.
    - http://wsgi.tutorial.codepoint.net/
    - https://wsgi.readthedocs.io/en/latest/learn.html

### Resources

- **books** - [1](https://www.amazon.com/Lightweight-Django-Using-WebSockets-Backbone/dp/149194594X/ref=sr_1_26?ie=UTF8&qid=1502139321&sr=8-26&keywords=python+web+application) [2](https://www.amazon.com/Flask-Web-Development-Developing-Applications/dp/1449372627/ref=sr_1_1?ie=UTF8&qid=1502136439&sr=8-1&keywords=python+web+application) [3](https://www.amazon.com/Python-Projects-Laura-Cassell/dp/111890866X/ref=sr_1_15?ie=UTF8&qid=1502136439&sr=8-15&keywords=python+web+application) [4](https://www.amazon.com/Building-Applications-Flask-Italo-Maia/dp/178439615X/ref=sr_1_16?ie=UTF8&qid=1502136439&sr=8-16&keywords=python+web+application) [5](https://www.amazon.com/Flask-Framework-Cookbook-Shalabh-Aggarwal/dp/178398340X/ref=pd_bxgy_14_img_2?_encoding=UTF8&pd_rd_i=178398340X&pd_rd_r=TFF5ES198Y5BZE6DQ2AF&pd_rd_w=OMA9P&pd_rd_wg=AvY9v&psc=1&refRID=TFF5ES198Y5BZE6DQ2AF) [6](https://www.amazon.com/Introduction-Tornado-Modern-Applications-Python/dp/1449309070/ref=sr_1_4?ie=UTF8&qid=1502136439&sr=8-4&keywords=python+web+application)
- **example projects**
[1](https://github.com/heroku-examples/python-websockets-chat) [2](https://github.com/nellessen/Tornado-Redis-Chat)
- **tutorials**
[1](**https://docs.djangoproject.com/en/1.11/intro/tutorial01/**) [2](https://ferretfarmer.net/2013/09/05/tutorial-real-time-chat-with-django-twisted-and-websockets-part-1/) [3](http://www.bogotobogo.com/python/python_network_programming_tcp_server_client_chat_server_chat_client_select.php) [4](https://code.tutsplus.com/tutorials/creating-a-web-app-from-scratch-using-python-flask-and-mysql--cms-22972)
- **hackernews**
[1](https://news.ycombinator.com/item?id=11181628) [2](https://news.ycombinator.com/item?id=11932417) [3](https://news.ycombinator.com/item?id=13463105) [4](https://news.ycombinator.com/item?id=11121355) [5](https://news.ycombinator.com/item?id=5234692)
- **stackoverflow**
[1](https://stackoverflow.com/questions/30604192/creating-a-real-time-chat-with-python-and-websocket) [2](https://stackoverflow.com/questions/20874391/django-python-real-time-peer-to-peer-chat-messaging?rq=1) [3](https://stackoverflow.com/questions/9371158/a-tutorial-for-a-web-based-chat-server-in-python) [4](http://aosabook.org/en/index.html)
- **videos**
[1](http://pyvideo.org/search.html?q=web+app)
- **all about web applications**
[1](https://python-guide-pt-br.readthedocs.io/en/latest/scenarios/web/) [2](https://wiki.python.org/moin/WebApplications) [3](https://docs.python.org/3.1/howto/webservers.html) [4](https://wiki.python.org/moin/WellKnownPythonPrograms)

