#  服务器mysql安装教程

1. ```shell
   wget https://dev.mysql.com/get/mysql80-community-release-el8-1.noarch.rpm
   ```

2. ```
   yum localinstall mysql80-community-release-el8-1.noarch.rpm 
   ```

3. ```
   yum update
   ```

4. ```
   yum install mysql-server
   ```

5. ```
    ps -ef | grep mysql  #查询mysql 进程
   ```

6. ```
   systemctl start mysqld
   systemctl enable mysqld
   systemctl status mysqld
   ```

7. ```
   /etc/my.cnf.d //mysql的启动配置文件
   * client.cnf //mysql客户端配置文件
   * mysql-server.cnf //mysql守护进程配置文件
   * mysql-default-authentication-plugin.cnf //默认权限授权配置文件
   备注：
   可复制一份到/etc下，修改成my.cnf
   ```

8. 重置密码

   ```
   use mysql; //选择数据库
   alter user 'root'@'localhost' identified by 'Aaqwer@1234';//修改密码 必须大小写加数字
   flush privileges; //刷新权限表
   备注：mysql8.0修改用户密码命令（新的修改方式）
   ```

9. 添加数据库

   ```
   create user 'wlxx'@'%' identified by 'Aaqwer@1234';
   create database wlxx;
   grant all privileges on ympay.* to 'wlxx'@'%';
   flush privileges;
   ```

10. 执行数据库导入 `source /tmp/xxx.sql`

11. 

