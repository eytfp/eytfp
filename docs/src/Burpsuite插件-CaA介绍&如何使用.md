# Burp suite插件\-CaA 介绍&如何使用

CaA 全称**Collector and Analyzer**，是**BurpSuite 专用流量收集、敏感信息提取、Web 信息挖掘、Fuzz 模糊测试一体化插件**，主打被动采集 HTTP 流量，提取参数、路径、接口、敏感字段，统计频次生成专属 Fuzz 字典，同时支持主动漏洞探测，是 Web 渗透、漏洞挖掘必备工具。
项目开源地址：[https://github\.com/gh0stkey/CaA](https://github.com/gh0stkey/CaA)

## 一、基础介绍

###  核心定位

基于 BurpSuite **Montoya API**开发，**被动采集 Proxy 代理流量**，自动提取：

- 请求参数：各种参数，如Query 参数、Form 表单、Cookie、JSON/XML 参数、敏感字段

- 路径信息：一级路径、完整 URL、接口端点、静态文件路径

- 数据统计：字段出现频次、参数值格式，生成目标专属字典

- 主动功能：内置 Fuzz 模块，探测隐藏参数、未授权接口、目录漏洞，联动 Burp Intruder 批量测试



## 二、详细安装步骤

**如果插件加载失败：那就是Burp 版本过低，升级至≥2023.12.1**

1. 下载插件 Jar 包：GitHub Releases 下载最新`CaA\.jar`

2. Burp 加载插件：

    - 顶部菜单：`Extender → Extensions → Add`

    - 加载类型选`Java`，选择下载的`CaA\.jar`，点击`Next`

      ![image-20260515132837283](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515132837283.png)

3. 加载成功：Burp 新增`CaA`标签页，首次加载自动生成数据库、配置文件

    ![image-20260515133032470](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515133032470.png)

    发现出现这个就是安装成功

    ![image-20260515133131481](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515133131481.png)



## 二、功能与使用

### 模块 1：Generator（被动敏感信息 / 流量收集）

**核心：开启 Burp 代理抓包，自动采集所有 HTTP 流量，全程后台静默运行**

1. 开启 Burp Proxy 代理，浏览器走代理访问目标网站
2. CaA 自动采集：

   - 参数：`id、username、mobilephone、token、cookie`等，提取手机号、身份证、账号密码等敏感信息

   - 路径：`/api、/login、/admin、/static`等接口 / 目录

   - 格式：统计参数值类型（数字、32 位 token、手机号、邮箱等）
3. 右键快捷操作：在 Burp 请求 / 响应面板，右键参数，可**复制 Raw/JSON/XML 格式敏感数据**，直接用于漏洞测试



**简而言之。就是你在浏览器开了代理比如说走127.0.0.1：8080这种burp suite默认代理的话，哪怕你不拦截，这个插件都会收集你浏览过多所有网页的各种敏感信息，字段，路径等等，你用内置浏览器就更轻松了。虽然你觉得没什么用，但是burp suite已经记录了**

**如下是我用内置浏览器访问一个靶场，我设置了不拦截**

![image-20260515144540749](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515144540749.png)

**但是你会在目标中看到如下信息，全部记录都被记录下来了，当你使用DataBoard搜索127.0.0.1:8080时，它会将这些网页的1敏感信息什么的都一次性提取出来**



![image-20260515144727816](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515144727816.png)

### 模块 2：DataBoard（敏感信息 / 数据看板，核心提取查询）

用于筛选域名，查看已采集的所有敏感信息、参数、路径、文件，按 Host 精准过滤

1. 进入`CaA → DataBoard`，输入目标**完整域名**（如`https://xxx\.com`）

2. 核心数据表（直接提取敏感信息）：

   - **Param（参数表）**：提取所有请求参数、敏感字段、出现频次，直接导出 Fuzz 字典

   - **File（文件表）**：提取 js、css、txt、备份文件，查找泄露的敏感文件

   - **Endpoint（接口表）**：提取后端接口端点，发现未授权接口

   - **FullPath（完整路径表）**：全量 URL 路径

   - **Path（一级路径表）**：根路径，用于目录爆破

   





注意看这里搜索的时127.0.0.1，而不是127.0.0.1:8080，因为端口只是表示不同的服务，只要有host即可，host相同代表是是同一个站点。

![image-20260515145817827](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515145817827.png)

### 模块 3：Generate（Payload 生成，联动 Burp Intruder）

1. 在 CaA 选中采集的敏感参数、路径，发送到`Generate`生成 Payload
2. 进入 Burp`Intruder → Payloads`，载荷类型选择`Extension\-generated`，选中`CaA Payload Generated`
3. 关闭`URL\-Encode`，批量测试参数越权、敏感信息泄露、接口未授权等漏洞



**随机抓一个包放到重放器重，然后发送，找到collectinfo，然后选择Send to Generator**
![image-20260515150606488](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515150606488.png)

**找到Generator，这里是生成payload，并且这种payload是给Burp suite自带的intrude用的**

![image-20260515150900689](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515150900689.png)

当我们生成payload后，我们来到intrude，然后选择如图所示的配置

![image-20260515151135685](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515151135685.png)



![image-20260515151831081](https://cdn.jsdelivr.net/gh/eytfp/Bed/img/img/image-20260515151831081.png)



不过这只是演示，并非实战，实际过程可能有点乱，如果碰到不会的或报错，记得多网上搜索，询问智能体AI，或是询问朋友！





## 四、实战使用技巧（挖洞高频用法）

1. **敏感信息提取**：搭配 HaE 插件（正则高亮敏感信息），CaA 采集字段 \+ HaE 高亮，**100% 精准提取手机号、身份证、密码、token、后台账号**

2. **字典定制**：用 DataBoard 导出目标参数，生成专属字典，Fuzz 命中率比通用字典提升 80%

3. **批量接口探测**：采集目标所有接口后，批量 Fuzz，快速发现未授权访问、越权漏洞

4. **离线迁移**：复制`CaA\.db`数据库文件，在其他 Burp 直接加载，复用已采集的敏感信息和字典

不过这里就先不提供具体的操作手法了，我也不是特别懂
