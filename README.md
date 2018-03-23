# mininet on Tinycore

## Porting mininet from Ubuntu to TinyCore

Please follow these steps to port mininet from Ubuntu to TinyCore linux

1. Go to tinycore box, install the python and python-setuptools as below:
```diff
+# tce-load -wi python-setuptools.tcz
+# tce-load -wi python.tcz
```
2. If tce-load timed-out, please do the following to give longer timeout for tce-load.

Please modify the file "/usr/bin/tce-load" for wget timeout as below. So that wget will not do default timeout. I increased to ~300sec as workaround. 
```diff
 snippet of changes:
 tc@box:/etc/init.d$ grep wget /usr/bin/tce-load
     wget -T 300 -cq "$MIRROR"/"$1".md5.txt 2>/dev/null
     wget -T 300 -c "$MIRROR"/"$1"
                     if (system("rm -f "depfile"; wget -T 300 -c -P "optional" "mirror"/"name".dep 2>/dev/null") == 0 && ! SUPPRESS)
```
3. Install mininet on your ubuntu linux box.

4. After installing the mininet in your ubuntu box, go the following location and make a copy of this file:
```diff
+# Location: /usr/local/lib/python2.7/dist-packages
+# File: "mininet-2.3.0d1-py2.7.egg"
```
5. Please copy the file "mininet-2.3.0d1-py2.7.egg" got from step-4 to your home directory in tinyCore box and execute the following command in tinycore:
```diff
+# tc@box:~$ sudo easy_install mininet-2.3.0d1-py2.7.egg
 Processing mininet-2.3.0d1-py2.7.egg
 Copying mininet-2.3.0d1-py2.7.egg to /usr/local/lib/python2.7/site-packages
 Adding mininet 2.3.0d1 to easy-install.pth file
 Installing mn script to /usr/local/bin
 
 Installed /usr/local/lib/python2.7/site-packages/mininet-2.3.0d1-py2.7.egg
 Processing dependencies for mininet===2.3.0d1
 Finished processing dependencies for mininet===2.3.0d1
```
6. copy "/usr/bin/mnexec" and "/usr/bin/mn" files from your ubuntu box to the folder "/usr/bin/" in tinycore linux box.

7. Execute mininet in tinycore linux as below
```
tc@box:/opt/vle/setup$ sudo mn 
*** Creating network
*** Adding controller
*** Adding hosts:
h1 h2 
*** Adding switches:
s1 
*** Adding links:
(h1, s1) (h2, s1) 
*** Configuring hosts
h1 h2 
*** Starting controller
c0 
*** Starting 1 switches
s1 ...
*** Starting CLI:
mininet> exit
*** Stopping 1 controllers
c0 
*** Stopping 2 links
..
*** Stopping 1 switches
s1 
*** Stopping 2 hosts
h1 h2 
*** Done
completed in 5.542 seconds
```

In order to make the changes persistent, use bootlocal.sh and filetool.sh scripts.
