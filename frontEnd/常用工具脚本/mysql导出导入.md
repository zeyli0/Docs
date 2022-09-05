# MYSQL导出导入



## 导出

### 导出结构

```shell
mysqldump -h192.168.78.2 -uwordpress2 -p --opt -d wordpress  > wordpress.sql 
mysqldump -h192.168.78.2 -uroot -p  --databases draft --no-data > draft-create.sql
```

```
mysqldump -h192.168.78.2 -uroot -p  draft table1 table2 table3 > draft.sql
```



### 导出结构和数据

```shell
mysqldump -h192.168.56.217 -uroot -p --databases runoob_db > runoob_db.sql

 
```

 

## 导入

```
$
```



