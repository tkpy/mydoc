linux环境搭配和处理
=========================

安装python3.5 
-----------------

安装python3.5可能使用的依赖
------------------------------
::

	apt-get install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel


到python官网找到下载路径, 用wget下载
----------------------------------------

::

	wget https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tgz

	#解压
	tar -zxvf Python-3.5.1.tgz


	cd Python-3.5.1               
	./configure --enable-shared --prefix=/usr/local
	make && make altinstall

搭建python3开发环境
--------------------------

1.安装virtualenv
----------------------

::

	pip install virtualenv

创建虚拟环境
------------------

:: 

	virtualenv -p /usr/local/bin/python3.4 py34env

激活虚拟环境
---------------

::

	source py34env/bin/activate

在虚拟环境中安装ipython
---------------------------
::

	pip install ipython

如果安装过程中提示如下错误： 

Can't connect to HTTPS URL because the SSL module is not available. - skipping 
请安装以下库: 

::

	yum install openssl-devel 

然后重新编译安装Python： 

::

	./configure --prefix=/usr/local &&  make && make altinstall  

在虚拟环境中启动ipython

::

	ipython

退出虚拟环境

::

	deactivate
