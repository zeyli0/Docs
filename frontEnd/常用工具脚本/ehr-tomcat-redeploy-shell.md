## ehr部署启动脚本

ehr-tomcat-redeploy.sh

```shell
#!/bin/bash
# ehr-tomcat-redeploy
EHR_TOMECAT=/home/xxl/apps/tomcat7-ehrview2.1.4-10102
echo "close tomcat7-ehrview2.1.4-10102"
kill -9 $(ps -ef | grep tomcat7-ehrview2.1.4-10102 | grep -v grep | awk '{print $2}')
sleep 5
echo "unpacking ehrview-pj-2.1.0.tar"
tar xf ${EHR_TOMECAT}/webapps/ehrview/ehrview-pj-2.1.0.tar -C ${EHR_TOMECAT}/webapps/ehrview/ --exclude=WEB-INF/config/spring
echo "start tomcat7-ehrview2.1.4-10102"
${EHR_TOMECAT}/bin/startup.sh
echo "view log"
tail -f ${EHR_TOMECAT}/logs/catalina.out
```

ehr-tomcat-restart.sh

```shell
#!/bin/bash
# ehr-tomcat-restart
EHR_TOMECAT=/home/xxl/apps/tomcat7-ehrview2.1.4-10102
echo "close tomcat7-ehrview2.1.4-10102"
kill -9 $(ps -ef | grep tomcat7-ehrview2.1.4-10102 | grep -v grep | awk '{print $2}')
sleep 5
echo "start tomcat7-ehrview2.1.4-10102"
${EHR_TOMECAT}/bin/startup.sh
echo "view log"
tail -f ${EHR_TOMECAT}/logs/catalina.out
```

