数据集表添加EVENTID

哪些表添加eventid
```
select replace(table_name, '_DOC', '') recordclassifying
  from user_tab_comments
 where table_name like '%_DOC'
   and table_type = 'TABLE'

```

生成批量加EVENTID字段和建索引语句
```
--alter table CDH_ACCIDENT add eventid VARCHAR2(32);
--create index IDX_CDH_ACCIDENT_eventid on CDH_ACCIDENT (EVENTID);

select 'alter table ' || recordclassifying || ' add EVENTID VARCHAR2(32);',
       'create index IDX_' || recordclassifying || '_EVENTID on ' ||
       recordclassifying || ' (EVENTID);'
  from (select replace(table_name, '_DOC', '') recordclassifying
          from user_tab_comments
         where table_name like '%_DOC'
           and table_type = 'TABLE')
```
