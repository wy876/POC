## 青藤云 EDR 权限提升漏洞
```
青藤的测试 POC
local function save_python_info(ctx, info_table)
local proc_names = {"python.exe"}
local procs_ret = ctx.get_proc_list_info_rely(ctx, proc_names)
if next(procs_ret) == nil then
return
end
-- call get version
-- ... 省略无关代码
get_python_ver(proc) -- ... 省略无关代码
end
function get_python_ver(proc)
if proc == nil then
return "" end

if file_api.file_exists(proc.path) then
local cmdline = "\"" .. proc.path .. "\" -V"
local ret, output = common.execute_shell(cmdline)
if ret == 0 and output and output ~= "" then
return regex.match(output, "\\d.+\\d")
else
agent.error_log("get python version info error:" .. tostring(ret))
return "" end
end
End

```
