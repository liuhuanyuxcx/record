# 一、启动mysql容器
	docker run --name yhbaas -p 35002:3306 -v /data/docker/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /data/docker/mysql/logs:/logs -v /data/docker/mysql/data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD='zaq1xsw@' -d mysql:5.7
# 二、mysql设置支持插入中文
## 1.登录数据库
	mysql -D databasename -u username -p
## 2.修改数据库设置，支持utf8
	mysql> show variables like'%char%'
	    -> ;
	+--------------------------------------+----------------------------+
	| Variable_name                        | Value                      |
	+--------------------------------------+----------------------------+
	| character_set_client                 | utf8                       |
	| character_set_connection             | utf8                       |
	| character_set_database               | latin1                     |
	| character_set_filesystem             | binary                     |
	| character_set_results                | utf8                       |
	| character_set_server                 | latin1                     |
	| character_set_system                 | utf8                       |
	| character_sets_dir                   | /usr/share/mysql/charsets/ |
	| validate_password_special_char_count | 1                          |
	+--------------------------------------+----------------------------+
	9 rows in set (0.00 sec)
	 
	mysql> set character_set_database=utf8;                   <strong>#更改编码属性</strong>
	Query OK, 0 rows affected, 1 warning (0.00 sec)
	 
	mysql> set character_set_server=utf8;
	Query OK, 0 rows affected (0.00 sec)
	 
	mysql> set character_set_client=utf8;
	Query OK, 0 rows affected (0.00 sec)
	 
	mysql> set character_set_connection=utf8;
	Query OK, 0 rows affected (0.00 sec)
	 
	mysql> set character_set_client=utf8;
	Query OK, 0 rows affected (0.00 sec)
	 
	mysql> set character_set_connection=utf8;
	Query OK, 0 rows affected (0.00 sec)
	 
	mysql> show variables like'%char%'
	    -> ;
	+--------------------------------------+----------------------------+
	| Variable_name                        | Value                      |
	+--------------------------------------+----------------------------+
	| character_set_client                 | utf8                       |
	| character_set_connection             | utf8                       |
	| character_set_database               | utf8                       |
	| character_set_filesystem             | binary                     |
	| character_set_results                | utf8                       |
	| character_set_server                 | utf8                       |
	| character_set_system                 | utf8                       |
	| character_sets_dir                   | /usr/share/mysql/charsets/ |
	| validate_password_special_char_count | 1                          |
	+--------------------------------------+----------------------------+
	9 rows in set (0.00 sec)
	 
	mysql> use test1
	Reading table information for completion of table and column names
	You can turn off this feature to get a quicker startup with -A
	 
	Database changed

	mysql> show tables;
	+-----------------+
	| Tables_in_test1 |
	+-----------------+
	| address         |
	| authors         |
	| book_m2m_author |
	| books           |
	| customer        |
	| student         |
	| study_record    |
	+-----------------+
	7 rows in set (0.00 sec)
	 
	mysql> insert into books (name) value('我');
	ERROR 1366 (HY000): Incorrect string value: '\xE6\x88\x91' for column 'name' at row 1
	mysql> alter table books convert to character set utf8;           <strong>#将数据表的编码方式改成utf8</strong>
	Query OK, 3 rows affected (0.02 sec)
	Records: 3  Duplicates: 0  Warnings: 0
	 
	mysql> insert into books (name) value('我');
	Query OK, 1 row affected (0.01 sec)
	 
	mysql> select * from books;
	+----+------+----------+
	| id | name | pub_date |
	+----+------+----------+
	|  1 | bbu1 | NULL     |
	|  2 | bbu2 | NULL     |
	|  3 | bbu3 | NULL     |
	|  4 | 我   | NULL     |
	+----+------+----------+
	4 rows in set (0.00 sec)
## 3.修改配置文件
###	1）编辑MySql的配置文件
MySql的配置文件Windows下一般在系统目录下或者在MySql的安装目录下名字叫my.ini，可以搜索，Linux下一般是/etc/my.cnf
	
	--在 [mysqld] 标签下加上以下内容
	character_set_server = utf8	
	注意：如果此标签下已经存在“default-character-set=GBK”类似的内容，只需修改即可。
	
	--在 [mysql]  标签下加上一行	
	default-character-set = utf8	

	--在 [mysql.server]标签下加上一行
	default-character-set = utf8

	--在 [mysqld_safe]标签下加上一行
	default-character-set = utf8	 
	
	--在 [client]标签下加上一行	
	default-character-set = utf8

### 2）重新启动MySql服务
	Windows可在服务管理器中操作，也可使用命令行：
	net stop mysql 回车
	net start mysql 回车
	服务名可能不一定为mysql，请按自己的设置
	Linux下面可是用 service mysql restart
	如果出现启动失败，请检查配置文件有没有设置错误
### 3）查看设置结果
	登录MySql命令行客户端：打开命令行	
	mysql –uroot –p 回车	
	输入密码	
	进入mysql后 执行 ：show variables like "%character%";
	显示结果应该类似如下：	
	| character_set_client | utf8 |	
	| character_set_connection | utf8 |	
	| character_set_database | utf8 |	
	| character_set_results | utf8 |	
	| character_set_server | utf8 |	
	| character_set_system | utf8 |	
	| character_sets_dir | /usr/share/mysql/charsets/ |	 
## 4.参考链接
[centos7中mysql不能输入中文问题的解决](https://www.cnblogs.com/qiangayz/p/8685917.html)