ehrview 清空数据



日志删除

```sql
select 'delete ' || table_name || ' ;'
  from user_tab_columns
 where column_name = 'DCID'
   and table_name in (select table_name
                        from user_tab_comments tt
                       where tt.table_type = 'TABLE');
```



无日志删除，不可恢复

```sql
select 'truncate table ' || table_name || ' ;'
  from user_tab_columns
 where column_name = 'DCID'
   and table_name in (select table_name
                        from user_tab_comments tt
                       where tt.table_type = 'TABLE');
```



清空浏览历史记录

```sql
truncate table SYS_BROWSINGHIST;
```

