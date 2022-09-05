## ORACLE导出导入

## 导出

直接命令导出

```
 exp lucy/bsoft@10.10.2.207:1521/orcl file=/home/usershare/lucy.dmp owner=lucy
 exp lucy/lucy@127.0.0.1/orcl tables=(weather) file=lucy.dmp owner=lucy
```

根据文件配置导出

```
$cat plsexp.par.lucy
log=/tmp/plsexp.log
file=lucy.dmp
userid=lucy/lucy@127.0.0.1/orcl
buffer=4096
tables=(weather)
compress=yes
consistent=no
grants=no
indexes=yes
rows=yes
triggers=yes
constraints=yes

```

```
exp parfile=plsexp.par.lucy
```



## 导入

```
imp lucy/lucy@127.0.0.1/orcl file=lucy.dmp fromuser=lucy touser=lucy IGNORE=Y LOG=import.log
```



#### 注意

先处理没有记录的表，防止无法导出表

``` {.sql}
select 'alter table '||table_name||' allocate extent;' from user_tables where num_rows=0
```