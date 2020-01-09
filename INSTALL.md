# INSTALLATION for Network Simulator 3

I run NS3 under Debian 10 (buster) (4.19.0-6-amd64 #1 SMP Debian 4.19.67-2+deb10u2 (2019-11-11) x86_64 GNU/Linux).

## Replace default "Python" to "Python 3"

Ref: https://www.linuxprobe.com/debian-switch-python.html

Use **update-alternatives** command to update python for the whole system.  

### Step 1: Install Python3 for system

```bash
sudo apt install python3
```

Package **python3** is available under Debian Buster. If you cannot find the corresponding package under the Linux distribution you are using, please install it manually.

### Step 2

**Command** 

```bash
sudo update-alternatives --list python 
```

**Result** 

```
update-alternatives: error: no alternatives for python 
```

That means the current python version has not been recognized by system, so you need to add the python version to system manually. 

Here is the sample code. Replace it to your own, modify it according to your system

```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.7 1
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2
```

### Step 3

Update the system's default python version. Now python packages can be recognized by system.  

```bash
sudo update-alternatives --list python
```

Then check it.

```bash
python -V
```

### Appendix

How to remove the added alternatives. 

```bash
# Update
sudo update-alternatives --list python
# Remove 
sudo update-alternatives --remove python /usr/bin/python3.7
```

# Run Network Simulator 3

## Update or install system requirements

```bash
sudo apt install gcc g++ gdb mercurial bzr valgrind gsl-bin libgsl0-dev libgsl0ldbl
sudo apt install flex bison tcpdump sqlite sqlite3 libsqlite3-dev
sudo apt install libxml2 libxml2-dev libgtk2.0-0 libgtk2.0-dev
sudo apt install vtun lxc uncrustify doxygen graphviz imagemagick
sudo apt install texlive texlive-latex-extra texlive-generic-extra texlive-generic-recommended texinfo dia texlive-extra-utils  python3-pygraphviz libboost-filesystem-dev
```

If the corresponding rpm package cannot be found, just delete it. 

If you use Redhat distribution, please change to yum yourself.  

## Clone NS3 from GitHub

```bash
git clone https://github.com/nsnam/ns-3-dev-git
```

## Test

```bash
./waf -d debug --enable-examples --enable-tests configure
./waf
```

## Build and Run First App

```bash
# Build
cp examples/tutorial/first.cc scratch/myfirst.cc
./waf
# Run
./waf --run scratch/myfirst
```

