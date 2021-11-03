# 操纵MySQL命令

- 启动MySQL

  ```service mysql start```

  

- 查看MySQL运行状态

  ```service mysql status```  或  ```service mysqld status```

  

- 连接本地服务器

  ``` sudo mysql -u root -p```

- 连接远程服务器
  ``` sudo mysql -h 10.2.130.242 -u xuesheng -p```

> mysql  -h  服务器地址xxx  -u  用户名xxx  -p密码xxx
>
> 不填则不写，如mysql -u root -p，没有写-h
>
> **-p后面没有空格**，紧接着写密码，其他可以写空格



- 改变数据库的默认字符集
  ```create database xxx default character set utf8 collate utf8_general_ci```



- 改变表的某字段长度

  ``` alter table 表名  modify column 字段名 var(8)```



# 云服务器安装MySQL

- 登陆云服务器

  > ```ssh root@47.96.141.152  ```

- 检查是否带有MySQL

  > ```sudo netstat -tap | grep mysql```
  >
  > 没显示，则未安装

- 安装MySQL

  > 先更新仓库
  >
  > ```