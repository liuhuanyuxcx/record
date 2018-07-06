# 安装postgresql
## 1.Install the repository RPM
	yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-redhat95-9.5-3.noarch.rpm
## 2.Install the client packages
	yum install postgresql95
## 3.install the server packages
	yum install postgresql95-server
## 4.initialize the database and enable automatic start
	/usr/pgsql-9.5/bin/postgresql95-setup initdb
	systemctl enable postgresql-9.5
	systemctl start postgresql-9.5
## 5.PostgreSQL 8.1 中文文档
[http://www.php100.com/manual/PostgreSQL8/app-psql.html]()
## 6.登录设置
	vi /var/lib/pgsql/9.5/data/pg_hba.conf
	#将登录认证方式改为trust
	local   all             all                                     trust
	# IPv4 local connections:
	host    all             all             127.0.0.1/32            trust
## 7.psql登录
	psql -U username -d database
	