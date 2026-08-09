# 本地预览

不要直接双击 `index.html`。这个静态网站使用以 `/` 开头的资源路径，必须通过本地 HTTP 服务器预览。

在解压后的根目录打开终端。该目录内应能直接看到 `index.html`、`_next` 和 `media`。

macOS / Linux：

```bash
python3 -m http.server 8000
```

Windows：

```powershell
py -m http.server 8000
```

然后打开：

`http://localhost:8000/`

Work 页面：

`http://localhost:8000/work/`

Field Notes 页面：

`http://localhost:8000/field-notes/`
