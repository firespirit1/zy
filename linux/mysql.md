MySql的个人配置存放在 /etc/mysql/my.cnf

daemon 守护进程，一般是服务器进程后面带的`d`

例如：

`mysqld --daemo`

mysql -h 主机 -P指定的端口号 -u 用户 -p密码

-h是主机host（ip地址）

-P是指定端口号

 -u 用户

 -p密码

mysql> GRANT ALL PRIVILEGES on *.* to 'zy'@'localhost' IDENTIFIED BY "123"WITH GRANT OPTION;

 flush privileges

![1567432948857](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1567432948857.png)

第一句是create