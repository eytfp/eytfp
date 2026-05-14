# 示例：Crypto 编码识别

<div class="post-meta"><strong>分类</strong>：CTF &nbsp;|&nbsp; <strong>标签</strong>：<code>Crypto</code> <code>编码</code></div>

## Base64 特征

- 字母表 `A-Za-z0-9+/`，填充 `=`
- 长度通常为 4 的倍数

## Hex

- `[0-9a-fA-F]{32,}` 常见于哈希或二进制转写

```python
import base64
base64.b64decode("ZmxhZ3tleGFtcGxlfQ==")
```
