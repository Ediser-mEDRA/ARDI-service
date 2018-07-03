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
