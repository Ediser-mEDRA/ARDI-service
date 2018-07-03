**Table of contents**

[TOCM]

# Install python and pip as local user
Since a linux user do not have root access, and need to install a local python an pip for its own needs, the following recipes describes some tips to do for the configuration:

## Install python to local directory
Firstly i create a folder in my local directory and download a python distribution that meets the desired requirements in the official [python download mirror](https://www.python.org/ftp/python/ "Python download mirror")

````
mkdir /development/python
cd /development/python
wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
tar zxfv Python-2.7.14.tgz
````
The next step is to change the directory, and move in the unzip directory

````
cd /development/python/Python-2.7.14
````
and ready to configure, compile and install the source following its guideline
````
./configure --prefix=/development/python/2.7.14
make && make install
````
Notice that the option `--prefix=/development/python/2.7.14` is required for this to work. By default, the `make` install all required python files to run in the following directory `/usr/local/` where the user does not get the permission to gather files, so the correct situation is to instruct the installation process to store the required python files to run in an appropriate directory.

Once the installation is done successfully, the linux shell must be instruct to work with the new python installed, and to achieved that, the user must edit the file 
`vi /development/.bashrc` to set the environment variable:

```
export PATH=/development/python/Python-2.7.14/bin:$PATH
export PYTHONPATH=/development/python/Python-2.7.14
```
Save the file and finally refresh the current shell session with the comand:
`source /development/.bashrc`
At this point the user must logout to the current shell and open a new one. In the new shell, the user must login with his credentials and verify that the new version of python have to be different to the former one if in the system there is already a python version.
The following comand `which python` allow to check it.
It should show the path to the python binary file, which is located in the directory: 
`/development/python/Python-2.7.14/python`

## Install pip in local directory as user different than root

The package installation manager for python to be install required the OpenSSL library. Install it first in a chosen local directory by 
performing the following steps:
    
   * Get the required or choose an distribution of OpenSSL
   
      ````
        mkdir /development/python/openssl
        cd /development/python/openssl
        wget https://www.openssl.org/source/openssl-1.1.0h.tar.gz
        tar zxvf openssl-1.1.0h.tar.gz 
      ````
      
   * Ready to configure, compile and install the source following its guideline
    
      ````
        mkdir local
        ./config --prefix=/development/python/openssl/local --openssldir=/development/python/openssl/local
        make && make install
      ````
    
Have a look on the documentation [here](https://github.com/openssl/openssl/blob/OpenSSL_1_0_2-stable/INSTALL) for any other configuration 
before the OpenSSL configuration and installation.
To verify if the installation is done successfully, run the following command: `openssl version` that display in shell windows the version 
installed.

After the shell must be instructed to use the new OpenSSL library with the following command:
`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/development/openssl/local/lib` 
or another solution could the settings of the command in the `vi .bashrc`. 

* Get the required pip python file in order to install the latest or a specific distribution

   ````
      cd /development/python/
      wget https://bootstrap.pypa.io/get-pip.py -o get-pip.py
      
   ````
1. If the user location from which python is installed doesn't required TLS/SSL, then run the following command to install pip
`python get-pip.py 'pip>6'` and the pip 1.5.6 version will be install or just run `python get-pip.py` to install the latest distribution.

2. Otherwise, pip is configured with locations that require TLS/SSL, so the ssl module in the local Python installed should be abilitated 
before fetching the pip installation from [URL](https://pypi.python.org/simple/pip/).

To achieve it, the following steps must be fullfilled:
 
 * Open Modules/Setup, and un-comment following part and save the file after
 
   ````
      vi /development/python/Python-2.7.14/Modules/Setup
      #SSL=development/python/openssl/local
      #_ssl _ssl.c \
      #       -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
      #       -L$(SSL)/lib -lssl -lcrypto
      
   ````
   
   * Compile and install again the Python
      
      ** `make & make install` python from source code 
      
      ** then run the following command to install pip `python get-pip.py 'pip>6'` and the pip 1.5.6 version will be install or just run 
      `python get-pip.py` to install the latest distribution.
