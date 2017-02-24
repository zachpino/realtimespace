### Controlling the Cache

---

Contemporary browsers do their best to avoid downloading already-consumed -- and therefore redundant -- files. This behavior can cause our map to not update correctly in all browsers (especially Chrome on Windows which is highly aggressive in its caching). These lines in the `<head>` tag should prevent all content on the page from being cached.

```
<meta http-equiv="cache-control" content="max-age=0" />
<meta http-equiv="cache-control" content="no-cache" />
<meta http-equiv="expires" content="0" />
<meta http-equiv="expires" content="Tue, 01 Jan 1980 1:00:00 GMT" />
<meta http-equiv="pragma" content="no-cache" />
```
