# 示例：Kerberos 速记

<div class="post-meta"><strong>分类</strong>：内网 &nbsp;|&nbsp; <strong>标签</strong>：<code>AD</code> <code>Kerberos</code></div>

## 票据速记

| 票据 | 简述 |
| --- | --- |
| TGT | 由 KDC 签发，用于申请 TGS |
| TGS | 用于访问具体服务 |

## 与审计/防御相关关键词

`AES256-SHA1`、`RC4`、`SPN`、`委派`

```text
Client -> AS: 请求 TGT
Client -> TGS: 用 TGT 换 TGS
Client -> Service: 用 TGS 访问服务
```
