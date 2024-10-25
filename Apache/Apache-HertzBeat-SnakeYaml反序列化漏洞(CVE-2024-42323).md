# Apache-HertzBeat-SnakeYaml反序列化漏洞(CVE-2024-42323)

Apache HertzBeat 是开源的实时监控工具。受影响版本中由于使用漏洞版本的 SnakeYAML v1.32解析用户可控的 yaml 文件，经过身份验证的攻击者可通过 /api/monitors/import、/api/alert/defines/import 接口新增监控类型时配置恶意的 yaml 脚本远程执行任意代码。

## 漏洞复现

访问http://localhost:4200/，admin/hertzbeat登录后台，选择任何监控点击导入监控

![image-20241009211426283.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250931543.png)

修改上传yaml文件中的value值：

![image-20241009211949488.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250931481.png)

成功执行代码

![image-20241009211904763.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250931374.png)



## 漏洞来源

- https://forum.butian.net/article/612