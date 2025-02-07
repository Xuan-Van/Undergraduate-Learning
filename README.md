# 目录

1. [Big Data Application](Big%20Data%20Application)：基于 Linux，介绍大数据应用平台的基础知识和相应操作。
2. [C](C)：30 个入门级脚本，基于 Windows Powershell 窗口运行。
3. [Data Structure](Data%20Structure)：使用 C 语言实现的 9 个数据结构项目，文章用 LaTeX 编写。
4. [Java](Java)：双色球福利彩票系统，在命令行输入 `java -jar Lottery.java` 即可运行。
5. [Mathematical Modeling](Mathematical%20Modeling)：使用 LaTeX 编写的 14 篇数学建模文章。
6. [PyMySQL](PyMySQL)：基于 Django，用 Python 将 Web 网页连接到 MySQL 数据库服务器的接口。
7. [Python](Python):
    - 30 个入门级脚本，基于 Windows Powershell 窗口运行。
    - 使用 Jupyter Notebook 文件，实现苏州大学 MOOC 中 Python 程序设计的教学内容。

# Big Data Application

## Linux

1. 基础操作：
    - 打开终端：`Ctrl+Alt+F1`
    - 权限提升：使用 `sudo` 命令
    - 关机：`sudo poweroff`
    - 关闭可视化界面：`sudo service lightdm stop`
    - 软件安装与更新：
        * 安装软件：`sudo apt-get install`
        * 更新软件包列表：`sudo apt-get update`
        * 安装远程登录系统：`sudo apt-get install openssh-server`
        * 安装编译工具：`sudo apt-get install build-essential`
2. 系统管理：
    - 查看所有进程：`sudo ps -aux`
    - 列出所有文件和目录：`ll`
    - 查看 IP 地址：`ifconfig`
    - 查看硬盘存储情况：`df -h`
    - 计算器：`bc`
    - 配置文件目录：`/etc`
3. 文件权限与类型：
    - 权限修改：
        * 解除文件的读写权限：`chmod -rw 文件名`
        * 为文件开启可读、可写、可执行权限：`chmod 777 文件名`
    - 文件类型颜色标识：
        * 普通文件：白色
        * 文件夹：蓝色
        * 可执行文件：绿色
4. 文件操作：
    - 重定向：
        * 覆盖文件内容：`>`
        * 追加内容到文件：`>>`
    - 管道，将前面命令的输出作为后面命令的输入：`|`
5. 文件系统：
    - 块设备文件：b 开头
    - 删除空文件夹：`rmdir`
    - tar 压缩：`tar czvf 文件名 文件夹名`
    - tar 解压：`tar xzvf 文件名`
    - jar 解压：`jar xvf 文件名`
    - rar 解压：`unrar e 文件名`
6. 文本处理：
    - 从尾行到头行显示文件内容：`tac 文件名`
    - 统计字符数：`wc 文件名`
    - 排序：`sort`
    - 显示程序最后退出状态（0 表示正常，127 表示异常）：`echo $?`
    - 将字符串作为程序的输入：`echo 句子 | python hello.py`

## 运行编程语言

1. 运行 Python：`python hello.py`
2. 编译 C：`gcc hello.c -o hello`
3. 运行 exe：`./hello`
4. 编译 Java：`javac hello.java`
5. 运行 Java：`java hello`

## nano 编辑器

1. 保存：`Ctrl+O`
2. 退出：`Ctrl+X`
3. 撤销：`Ctrl+U`
4. 删除：`Ctrl+K`

## Hadoop

|          效果           |                         指令                         |
| ----------------------- | --------------------------------------------------- |
| 登录自己的服务器         | `ssh 127.0.0.1`（127.0.0.1 是本机 IP 地址）           |
| 首次启动格式化 HDFS      | `hdfs namenode -format`                             |
| 启动 Hadoop 集群         | `$HADOOP_HOME/sbin/start-all.sh`                    |
| 显示端口使用情况         | `netstat -tupln`                                    |
| HDFS 命令行工具         | `hadoop fs`                                         |
| 创建 HDFS 目录           | `hadoop fs -mkdir /`                                |
| 从本地复制文件到 HDFS    | `hadoop fs -copyFromLocal /home/xuan/mybash /test/` |
| 将本地文件放到 Hadoop 中 | `hadoop fs -put /home/xuan/bigdata/u.item /bigdata` |
| 查看 HDFS 中的所有子目录 | `hadoop fs -ls -R /`                                |

## PySpark

1. 基本操作：
    - 退出 PySpark：`quit()`
    - 读取文件：`data = sc.textFile("文件路径")`
    - 运行脚本（本地 k 线程运行）：`spark-submit --driver-memory=1g --master local[k] 文件名`
2. RDD操作：
    - 列表转 RDD：`rdd = sc.parallelize(list)`
    - RDD 转回原形式：`rdd.collect()`
    - 映射操作，对 RDD 的每个元素执行函数：`rdd.map(函数名)`
    - 过滤操作，根据条件过滤元素：`filter(lambda x:条件)`
    - 截取 n 组数据：`take(n)`
    - 首字母大写：`rdd1 = sc.parallelize(b).map(lambda x: x[0].upper() + x[1:]).collect()`
    - 保留 5<=x<=10 的值：`rdd1 = sc.parallelize(a).filter(lambda x: x >= 5 and x <= 10).collect()`
    - 统计字数：`count = sc.parallelize(a.split()).map(lambda x: (x, 1)).reduceByKey(lambda x, y: x + y).collect()`
3. 数据处理示例：
    - 电影平均分计算：
        ```python
        data1 = data.map(lambda x: x.split('\t')[0:3])
        data2 = data1.map(lambda x: (x[1], x[2]))
        data3 = data2.map(lambda x: (x[0], (int(x[1]), 1)))
        data4 = data3.reduceByKey(lambda x, y: (x[0] + y[0], x[1] + y[1]))
        data5 = data4.map(lambda x: (x[0], float(x[1][0]) / x[1][1]))
        ```
    - 每个人打电影的平均分：`data2 = data1.map(lambda x: (x[0], x[2]))`
4. CSV 文件处理：
    - 读取 CSV 文件：
        ```python
        data = sc.textFile("file:文件路径")
        header = data.first()
        rawdata = data.filter(lambda x: x != header)
        rd = rawdata.map(lambda x: x.split(','))
        ```
    - 删除第一列：`rd = rawdata.map(lambda x: x.split(',')[1:])`
    - 列去重并索引化：`cm = rd.map(lambda x: x[4]).distinct().zipWithIndex().collectAsMap()`

# MYSQL

## 常用命令

|     描述      |                                                     对应指令或位置                                                     |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| 安装目录       | `C:\Program Files\MySQL\MySQL Server 5.6\bin`                                                                        |
| 登录          | `mysql -uroot -p123456 -h127.0.0.1` 或 `mysql -uroot -p123456 -hlocalhost -P3306`                                    |
| 创建数据库     | `create database bookmanage default charset gbk;` 或 `create database if not exists bookmanage default charset gbk;` |
| 查看所有数据库 | `show databases;`                                                                                                    |
| 修改          | `alter database bookmanage default charset utf8;`                                                                    |
| 删除          | `drop database bookmanage;` 或 `drop database if exists bookmanage;`                                                 |
| 帮助          | `\h`                                                                                                                 |
| 设置数据库编码 | `set names gbk;`                                                                                                     |
| 使用数据库     | `use xscj;`                                                                                                          |
| 显示表格       | `show table;`                                                                                                        |
| 显示表格结构   | `describe xs;` 或 `desc xs;`                                                                                         |
| 显示表格内容   | `select * from xs;`                                                                                                  |
| 导入语句       | `source 本地 .sql 文件路径`                                                                                            |
| 注释          | `-- ` 或 `/*  */`                                                                                                    |

## Python 连接数据库

```python
import numpy as np
import pandas as pd
from sqlalchemy import create_engine
import pymysql
engine = create_engine("mysql+pymysql://root:123456@localhost:3306/xscj")
data = pd.read_sql("select * from xs", con=engine)
data1 = pd.read_sql("select 成绩 from xs_kc where 课程号='101'", con=engine)
data1.describe()
```

## 乱码问题

- 显示：`show variables like '%char%';`
- 修改：`set character_set_database=gbk;`
- 配置文件的位置：`C:\ProgramData\MySQL\MySQL Server 5.6\my.ini`
