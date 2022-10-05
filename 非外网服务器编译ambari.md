## 非外网服务器编译ambari
### ambari-admin/pom.xml
```shell
            <configuration>
              <arguments>install --unsafe-perm</arguments>
            </configuration>

-->

            <configuration>
              <arguments>install --unsafe-perm --registry=http://registry.npm.taobao.org</arguments>
            </configuration>
```
### ambari-admin/src/main/resources/ui/admin-web/.bowerrc
```
{
    "directory": "app/bower_components"
}

--->

{
    "directory": "app/bower_components",
     "proxy" : "http://192.168.26.1:7890",
     "https-proxy" : "http://192.168.26.1:7890"
}
```
