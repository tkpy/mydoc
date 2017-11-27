修改linux的mysql密码
----------------------
	方法一：
	在mysql系统外，使用mysqladmin
	# mysqladmin -u root -p password "test123"
	Enter password: 【输入原来的密码】

	方法二：
	通过登录mysql系统，
::
	# mysql -uroot -p
	Enter password: 【输入原来的密码】
	mysql>use mysql;
	mysql> update user set password=passworD("test") where user='root';
	mysql> flush privileges;
	mysql> exit;  