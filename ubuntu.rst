Ubuntu
#######

.. contents::
  :local:
  :depth: 5


Fix capslock
-------------
- `(source) <http://www.noah.org/wiki/CapsLock_Remap_Howto>`_
- `(source) <https://help.ubuntu.com/community/NumLock>`_
- `(source) <https://help.ubuntu.com/community/NumLock>`_

# Numbering files (appended number)
for i in *.png
do
  mv $i ${i/.png/-0}
done

# Numbering files (prepended number)
for i in {1..9}
do
  mv file_$i `printf file_0$i`
done

# Monitor the job
watch -c -d -n 1 tail /var/log/syslog

# Downlaod a file
curl URL --output FILE

# DownloadURL  multiple files matching a patterns
curl URL 2> /dev/null |
  grep -iE '(FUCK|YOU)' |
  sed -E 's/^.*href="(.*)".*$/\1/' |
  while read line; do
  echo "http://www.whyprime.com/temp/destroy_all_software/"$line
  done

# Print the nth word (awk treats whitespace as word delimeters)
awk '{print $1}'

# image to pdf
convert IMAGEFILE{1..3}.jpg OUT.pdf
# txt to pdf
soffice --headless --convert-to pdf in.txt
# pdf to txt
pdftotext IN.pdf OUT.txt
# combine pdfs
pdfunite ./*.pdf OUT.pdf
# grep pdfs, recursively
pdfgrep -HiR 'pattern' /path
# giff pdfs
pdfdiff FILE1.pdf FILE2.pdf


Samba Windows Shares
--------------------

`(source) <http://www.configserverfirewall.com/ubuntu-linux/mount-samba-share-ubuntu-cifs/>`_
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


Manpages
--------
# yelp - browse and jump through manpage links
yelp man:grep
# groff - generate html manpage with groff, open with browser **(best for printing)**
sudo apt install groff
man --html=google-chrome-stable SOME_APPLICATION
# chrome 
sudo apt install txt2html
man SOME_APPLICATION | txt2html - | google-chrome-stable "data:text/html;base64,$(base64)"
#  lynx
sudo apt install man2html
zcat $(man --path 1 grep) | man2html -l | lynx -stdin
# w3m 
zcat $(man --path 1 grep) | man2html -l | w3m -T text/html

View Files From A Clonezilla Backup
-----------------------------------
# Extract into an image file
sudo su
cat sda2.ext4-ptcl-img.gz.* | gunzip -c | partclone.restore -s - -W -o./sda2.img

Dconf Settings
--------------

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
