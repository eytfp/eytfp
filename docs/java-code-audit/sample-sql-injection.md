# 示例：SQL 拼接风险

<div class="post-meta"><strong>分类</strong>：Java 代码审计 &nbsp;|&nbsp; <strong>标签</strong>：<code>SQLi</code> <code>MyBatis</code> <code>审计模板</code></div>

## 背景

求职笔记示例：记录一次代码审计中常见的 **字符串拼接 SQL** 模式。

## 危险写法

```java
String sql = "SELECT * FROM users WHERE id = '" + request.getParameter("id") + "'";
Statement st = conn.createStatement();
ResultSet rs = st.executeQuery(sql);
```

## 相对安全方向

- 参数化查询 / `PreparedStatement`
- ORM 中避免原生 SQL 拼接用户输入
- 白名单校验 + 最小权限

## 审计关键词（可搜代码）

`createStatement`、`executeQuery(`、`+ request`、`String sql`
