Source from
https://www.rosehosting.com/blog/how-to-install-python-3-6-4-on-centos-7/
https://www.cnblogs.com/zhangborsx/p/8549583.html

## Install from source
### Step 1 Install the development tools needed for compilation
First, we will need the tools in order to be able to compile and install programs from their source code. To do this, we will install the group “Development Tools” through Yum itself:
```
sudo yum groupinstall -y "Development Tools"
```
### Step 2: Download the Python source files.
First, we need to create a directory in which our install will take place. Make a directory with a name of your choosing, then enter the directory. Once you are in your new directory, enter the following command to download the compressed Python source file.
```
wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz
```
Once the file is finished downloading, uncompress the file by using tar, then enter into the new directory that was just created:
```
tar -xJf Python-3.6.4.tar.xz
cd Python-3.6.4
```
### Step 3: Run the configuration script.
Use the following command to have the installation software check your system before actually starting the installation process
```
./configure
```
First, we run the ‘make’ command which compiles the program.
```
make
```
Then, once that is finished, we can run the installation command.
```
make install
```

## 在centos7 中安装Python3中遇到的问题
```
wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
tar -xvf Python-3.6.4.tgz
cd Python-3.6.4
./configure
```

```
issue 1:
error message：
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details

Solve: 安装GCC
yum install gcc

issue 2:
zipimport.ZipImportError: can't decompress data; zlib not available
make: *** [install] Error 1

Solve: 
1. yum install -y zlib*
2. cd Modules/zlib  
3. ./configure
4. make install
finished, now you can continue install python
```
```
if the `pip` have problem below:
pip is configured with locations that require TLS/SSL

then  install openssl & openssl-devel
yum -y install openssl
yum -y install openssl-devel

when finished reinstall python
./configure --with-ssl 
make
sudo make install
```

