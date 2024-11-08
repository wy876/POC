## EyouCMS文件包含RCE漏洞

First, download the latest source code from the official website:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736654.png)
After downloading, use PHPStudy Pro to set up the website:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736275.png)
Proceed with the installation process, setting up the database information and admin password:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736805.png)
In the admin panel, verify that the current version is the latest:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736228.png)
Prepare a malicious payload in the form of an image, utilizing Remote Code Execution (RCE) via template file inclusion:

```
GIF89a
<?php phpinfo();?>
```
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736384.png)
Upload the image payload:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736923.png)
Choose the WeChat public account interface:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736602.png)
Proceed with the upload and obtain the returned path:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736696.png)

```
uploads/allimg/20230901/1-230Z1151QR14.gif
```
Return to the template configuration, set up security questions:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061736323.png)
After configuring security questions, edit the "index.htm" template under the PC section:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737706.png)Input the following payload:

```
{eyou:include file="uploads/allimg/20230901/1-230Z1151QR14.gif" /}
```
Append it at the end:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737598.png)
After submission:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737557.png)
Return to the homepage, where arbitrary code execution can be observed:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737266.png)

## Code Audit
Firstly, the `eyou:include` tag is present in the list of parsed tags, and there is no filtering mechanism applied to it:
```
core\library\think\Template.php
```
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737623.png)
The template file "index.htm" is read and stored in the `$content` variable. Parsing takes place in "core\library\think\Template.php":![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737286.png)
We can observe the `parseEyouInclude` function:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737366.png)
Inside this function, the template is analyzed and processed, where we can see that only string operations are performed, and no security risk evaluation is conducted:![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737380.png)
Finally, at the end, the tags are replaced and returned:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737460.png)
Due to the absence of security filtering, the include tag's parsing result directly reads and replaces content:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737841.png)
Similarly, in the "Template.php" file, writing to the cache occurs:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737357.png)
Digging deeper:

```
core\library\think\template\driver\File.php
```
In the `write` method, content is directly written:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737034.png)
Cache directory:
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061737865.png)
Ultimately, in the `read` method of "File.php," the temporarily generated file is included, leading to Remote Code Execution (RCE):

```
core\library\think\template\driver\File.php
```
![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061738568.png)