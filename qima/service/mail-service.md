本地启动之后，获取 ip,  更新
```sql
update PARM_GLOBAL_APP_CONFIG_LY set  PROP_VALUE='http://10.40.69.8:8081/mailx' where PROP_KEY='mail.service.url';
```

notion: application context is null 