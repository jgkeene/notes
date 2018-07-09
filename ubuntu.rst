Ubuntu
#######

.. contents::
  :local:
  :depth: 5



Keyboard Fixes
-----------------

- Capslock `(source) <http://www.noah.org/wiki/CapsLock_Remap_Howto>`_ 
- Numlock`(source) <https://help.ubuntu.com/community/NumLock>`_ 
- Numlock`(source) <https://help.ubuntu.com/community/NumLock>`_



Setting Up SMB Shares
----------------------

`(source) <http://www.configserverfirewall.com/ubuntu-linux/mount-samba-share-ubuntu-cifs/>`_

.. code-block:: bash

sudo apt install cifs-utils
# Manual mount via Nautilus
nautilus --select smb://192.168.0.3/nfs
# Results
$ mount | grep gvfsd-fuse
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)

# Automatic mount, via fstab
mkdir /media/azhee/nfs
sudo vim /etc/fstab
//192.168.0.3/nfs  /media/azhee/nfs  cifs  rw,_netdev,username=0,password=0,users  0 0
mount | grep cifs
//192.168.0.3/nfs on /media/azhee/nfs type cifs (rw,nosuid,nodev,relatime,vers=default,cache=strict,username=0,domain=,uid=1000,forceuid,gid=1000,forcegid,addr=192.168.0.3,file_mode=0755,dir_mode=0755,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,echo_interval=60,actimeo=1,_netdev)

View and Save Dconf Settings
-------------------------------

.. code-block:: bash

  # dump dconf settings
  dconf dump / >> ./dump.txt
  # restore dconf settings
  dconf load ./dump.txt

View Installed Software
-----------------------

.. code-block:: bash

# List all installed packages, with version numbers
apt list --installed
# Lists installed packages (excludes if installed as a dependency), with descriptions
aptitude search '~i!~M'
# Lists installed packages (excludes if installed as a dependency), without descriptions
aptitude search -F '%p' '~i'
# Shows the installation commands you used, with dates
(zcat $(ls -tr /var/log/apt/history.log*.gz); cat /var/log/apt/history.log) 2>/dev/null |
egrep '^(Start-Date:|Commandline:)' |
grep -v aptdaemon |
egrep -B1 '^Commandline:'
# Shows the installation commands you used, without dates
(zcat $(ls -tr /var/log/apt/history.log*.gz); cat /var/log/apt/history.log) 2>/dev/null |
egrep '^(Start-Date:|Commandline:)' |
grep -v aptdaemon |
egrep '^Commandline:'
