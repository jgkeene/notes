Currently Installed
```
libpython3-stdlib
libpython3.5
libpython3.5-minimal
libpython3.5-stdlib
python3
python3-apt
python3-brlapi
python3-cairo
python3-chardet
python3-cups
python3-cupshelpers
python3-dbus
python3-debian
python3-debianbts
python3-gi
python3-gi-cairo
python3-httplib2
python3-louis
python3-mako
python3-markupsafe
python3-minimal
python3-pexpect
python3-pil
python3-pkg-resources
python3-ptyprocess
python3-pyatspi
python3-pycurl
python3-pykde4
python3-pyqt4
python3-pysimplesoap
python3-renderpm
python3-reportbug
python3-reportlab
python3-reportlab-accel
python3-requests
python3-sip
python3-six
python3-smbc
python3-software-properties
python3-speechd
python3-uno
python3-urllib3
python3-xdg
python3.5
python3.5-minimal
```

Python3 sys.PATH
```
'/usr/lib/python35.zip',
'/usr/lib/python3.5',
'/usr/lib/python3.5/plat-x86_64-linux-gnu',
'/usr/lib/python3.5/lib-dynload',
'/usr/lib/python3/dist-packages'

'/usr/local/lib/python3.5/dist-packages'
```

Install tools system-wide
```
sudo python3 ./get-pip.py
```

Install virtualenv to local users
```
pip3 install --user virtualenv
```


Example of download/test/run someone's package
```
Get the HowDoI module from GitHub: 3
git clone XXX
virtualenv -p python3 venv
source venv/bin/activate
(venv)$ cd projects
(venv)$ pip install --editable .
(venv)$ python test_PROJECT.py # Run the unit tests.
```
