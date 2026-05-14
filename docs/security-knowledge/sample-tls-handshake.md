# 示例：HTTPS 握手速记

<div class="post-meta"><strong>分类</strong>：网安知识 &nbsp;|&nbsp; <strong>标签</strong>：<code>TLS</code> <code>HTTPS</code></div>

## 简化流程

1. ClientHello：支持的算法、随机数
2. ServerHello + Certificate + ServerHelloDone
3. 密钥交换与 Finished

## 面试常问

- 为什么需要三个随机数？
- 证书链校验在什么阶段完成？

```http
HTTP/1.1 200 OK
Strict-Transport-Security: max-age=31536000; includeSubDomains
```
