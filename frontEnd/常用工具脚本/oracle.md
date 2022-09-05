字符集转换
==========

-   AMERICAN\_AMERICA.AL32UTF8
-   SIMPLIFIED CHINESE\_CHINA.ZHS16GBK

查看数据库的字符集
==================

``` {.sql}
select * from v$nls_parameters;
select * from nls_database_parameters;

```

Oracle数据库的字符集更改
========================

``` {.sql}
[SQL> conn / as sysdba     --需要使用SYSDBA帐户
SQL>  startup mount
SQL>  shutdown immediate;   --停止数据库
SQL>  startup mount;         --启动数据库到 mount 状态
SQL> alter session set sql_trace=true;
SQL>  alter system enable restricted session;
SQL> alter system set job_queue_processes=0;
SQL> alter system set aq_tm_processes=0;
SQL> alter database open;
SQL>  ALTER DATABASE character set INTERNAL_USE AL32UTF8; --修改字符集AL32UTF8->ZHS16GBK
SQL> shutdown immediate;        --再次关闭数据库
SQL> STARTUP;            --启动数据库

```

Oracle11g创建表空间语句
=======================

分为四步

-   第1步：创建临时表空间

``` {.sql}
create temporary tablespace jack_temp
tempfile 'D:\oracledata\jack_temp.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;
```

- 第2步：创建数据表空间

    ```
    --查看已有表空间
    select * from dba_data_files
    ```

    ![](asserts\2020-04-24093920.png)

``` {.sql}
create tablespace jack_data
logging
datafile 'D:\oracledata\jack_data.dbf'
size 50m
autoextend on
next 50m maxsize 20480m
extent management local;
```

- 第3步：删除临时表空间或者表空间

  ```
   DROP TABLESPACE ECOLOGY INCLUDING CONTENTS AND DATAFILES;
  ```

  ECOLOGY 为要删除的表空间名；

-   第4步：创建用户并指定表空间

``` {.sql}
create user jack identified by jack
default tablespace jack_data
temporary tablespace jack_temp;
```

-   第5步：给用户授予权限

``` {.sql}
grant connect,resource,dba to jack;


```

用户默认表空间查询
==================

``` {.sql}
select username, default_tablespace from dba_users order by username;

```

导出导入
========

先处理没有记录的表，防止无法导出表

``` {.sql}
select 'alter table '||table_name||' allocate extent;' from user_tables where num_rows=0
```

常用导出，以jack为例

``` {.shell}
exp jack/jack@127.0.0.1/orcl file=c:\tmp\jack.dmp owner=jack
imp jack/jack@127.0.0.1/orcl file=c:\tmp\jack.dmp fromuser=jack touser=jack2 IGNORE=Y LOG=i.log
```

根据配置文件进行导出

``` {.text}
og=/tmp/plsexp.log
file=mystuff.dmp
userid=jack/jack@127.0.0.1/orcl
buffer=4096
tables=(mytable)
compress=yes
consistent=no
grants=no
indexes=yes
rows=yes
triggers=yes
constraints=yes
```

``` {.sql}
exp parfile=plsexp.par
```

非dba用户导出,创建用户,并授权

    create user jack IDENTIFIED BY jack123;
    GRANT EXP_FULL_DATABASE,IMP_FULL_DATABASE,
    DBA,CONNECT,RESOURCE,CREATE SESSION TO jack;

oracle 表空间使用情况
=====================

查询表空间使用情况
------------------

``` {.sql}
SELECT Upper(F.TABLESPACE_NAME)         "表空间名",
       D.TOT_GROOTTE_MB                 "表空间大小(M)",
       D.TOT_GROOTTE_MB - F.TOTAL_BYTES "已使用空间(M)",
       To_char(Round(( D.TOT_GROOTTE_MB - F.TOTAL_BYTES ) / D.TOT_GROOTTE_MB * 100, 2), '990.99')
       || '%'                           "使用比",
       F.TOTAL_BYTES                    "空闲空间(M)",
       F.MAX_BYTES         oracle 表空间使用情况             "最大块(M)"
FROM   (SELECT TABLESPACE_NAME,oracle 表空间使用情况
               Round(Sum(BYTES) / ( 1024 * 1024 ), 2) TOTAL_BYTES,
               Round(Max(BYTES) / ( 1024 * 1024 ), 2) MAX_BYTES
        FROM   SYS.DBA_FREE_SPACE
        GROUP  BY TABLESPACE_NAME) F,
       (SELECT DD.TABLESPACE_NAME,
               Round(Sum(DD.BYTES) / ( 1024 * 1024 ), 2) TOT_GROOTTE_MB
        FROM   SYS.DBA_DATA_FILES DD
        GROUP  BY DD.TABLESPACE_NAME) D
WHERE  D.TABLESPACE_NAME = F.TABLESPACE_NAME
ORDER  BY 1

```

查询表空间的free space
----------------------

``` {.sql}
select tablespace_name, count(*) AS extends,round(sum(bytes) / 1024 / 1024, 2) AS MB,sum(blocks) AS blocks from dba_free_space group BY tablespace_name;

```

查询表空间的总容量
------------------

``` {.sql}
select tablespace_name, sum(bytes) / 1024 / 1024 as MB from dba_data_files group by tablespace_name;

```

查询表空间使用率
----------------

``` {.sql}
SELECT total.tablespace_name,
       Round(total.MB, 2)           AS Total_MB,
       Round(total.MB - free.MB, 2) AS Used_MB,
       Round(( 1 - free.MB / total.MB ) * 100, 2)
       || '%'                       AS Used_Pct
FROM   (SELECT tablespace_name,
               Sum(bytes) / 1024 / 1024 AS MB
        FROM   dba_free_space
        GROUP  BY tablespace_name) free,
       (SELECT tablespace_name,
               Sum(bytes) / 1024 / 1024 AS MB
        FROM   dba_data_files
        GROUP  BY tablespace_name) total
WHERE  free.tablespace_name = total.tablespace_name;

```
