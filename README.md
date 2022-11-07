<h1 align="center">scalpel🗡</h1>

  ![go](picture/label/go-blue.svg)
  ![fuzz](picture/label/fuzz-blue.svg)
  ![pentest](picture/label/pentest-blue.svg)
  ![scanner](picture/label/scanner-blue.svg)
  
  > scalpel是一款命令行扫描器，它可以深度解析http请求中的参数，从而根据poc产生更加精确的http报文。目前支持http被动代理模式进行扫描。用户可以自定义POC，同时我们也在Github上公开了POC仓库。
  
 ![](https://github.com/StarCrossPortal/scalpel/blob/master/picture/demo.gif)


# 免责声明
本工具仅面向合法授权的安全测试和研究行为，**请勿对非授权目标进行扫描**。如您在使用本工具的过程中存在任何非法行为，您需自行承担相应后果，我们将不承担任何法律及连带责任。如您需要测试本工具的可用性，请自行搭建靶机环境。

为避免被恶意使用，本项目所有收录的poc均为漏洞的理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。

在安装并使用本工具前，**请您务必审慎阅读、充分理解各条款内容，限制、免责条款或者其他涉及您重大权益的条款**可能会以加粗、加下划线等形式提示您重点注意。您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。
# 检测模块
检测模块会不断进行更新，以支持检测更多的漏洞。
* CVE漏洞检测

  支持CVE系列漏洞检测

* XSS漏洞检测

  支持XSS漏洞检测

* SQL 注入检测

  支持报错注入、布尔注入等

* 命令/代码注入检测

  支持 shell 命令注入、 代码执行、模板注入等

* CRLF 注入 (key: crlf-injection)

  检测 HTTP 头注入，支持 query、body 等位置的参数

* 用友软件 系列漏洞检查

  检测使用的用友系统是否存在漏洞

* springboot 系列漏洞检测

  检测目标网站是否存在springboot系列漏洞

* Thinkphp系列漏洞检测

  检测ThinkPHP开发的网站的相关漏洞

* ...

# 功能特色

Scalpel支持**深度参数注入**，其拥有一个强大的数据解析和变异算法，它可以将常见的数据格式（json, xml, form等）解析为树结构，然后根据poc中的规则，对树进行变异，包括对叶子节点和树结构
的变异。变异完成之后，将树结构还原为原始的数据格式。

![](https://github.com/StarCrossPortal/scalpel/blob/master/picture/%E5%8F%82%E6%95%B0%E8%A7%A3%E6%9E%90.png)

解决在HTTP应用漏洞Fuzz过程中，**传统的「Form表单明文传参的模式」逐渐变为「复杂、嵌套编码的参数传递」** 无法直接对参数内容进行注入或替换，深入底层的漏洞触发点的问题。


# 快速使用


scalpel使用代理模式进行被动扫描，以Windows系统为例：



`.\scalpel-windows-amd64.exe poc -l 127.0.0.1:8888 -f poc.yaml -o vuln.html`




Scalpel的下载、运行、配置具体请参考[Wiki](https://github.com/StarCrossPortal/scalpel/wiki)



# POC相关

**POC的编写**


详情见[POC编写指南](https://github.com/StarCrossPortal/scalpel/wiki/POC%E7%BC%96%E5%86%99%E6%8C%87%E5%8D%97)


**POC贡献**


贡献者以 PR 的方式向 githuh 仓库内提交POC，在提交之前请搜索仓库的 poc 文件夹以及 Github 的 Pull request, 确保该 POC 没有被提交。


**POC参考**


目前scalpel已集成100+漏洞POC

| 类别        | CVE编号        | 漏洞名称                                            | 支持 |
| ----------- | -------------- | --------------------------------------------------- | ---- |
| CVE（2022） | CVE-2022-0540  | Jira身份验证绕过漏洞                                | ✔    |
| CVE（2022） | CVE-2022-22954 | VMware Workspace ONE Access SSTI RCE 漏洞           | ✔    |
| CVE（2022） | CVE-2022-26134 | Confluence OGNL RCE 漏洞                            | ✔    |
| CVE（2022） | CVE-2022-34590 | Hospital Management System SQL注入漏洞              | ✔    |
| CVE（2022） | CVE-2022-35151 | kkFileView v4.1.0 包含多个跨站点脚本 (XSS) 漏洞     | ✔    |
| CVE（2022） | CVE-2022-35413 | WAPPLES 硬编码漏洞                                  | ✔    |
| CVE（2022） | CVE-2022-35914 | GLPI 注入漏洞                                       | ✔    |
| CVE（2022） | CVE-2022-36642 | Telos Alliance Omnia MPX Node 信息泄露漏洞          | ✔    |
| CVE（2022） | CVE-2022-36883 | Jenkins 身份验证绕过漏洞                            | ✔    |
| CVE（2022） | CVE-2022-37299 | Shirne CMS controller.php 目录遍历漏洞              | ✔    |
| CVE（2021） | CVE-2021-26086 | Atlassian Jira server文件读取漏洞                   | ✔    |
| CVE（2021） | CVE-2021-29622 | Prometheus 重定向漏洞                               | ✔    |
| CVE（2021） | CVE-2021-30497 | Avalanche 目录遍历漏洞                              | ✔    |
| CVE（2021） | CVE-2021-33807 | Cartadis Gespage 目录遍历漏洞                       | ✔    |
| CVE（2021） | CVE-2021-34473 | Microsoft Exchange Server 远程代码执行漏洞          | ✔    |
| CVE（2021） | CVE-2021-35380 | Solari di Udine TermTalk Server 目录遍历漏洞        | ✔    |
| CVE（2021） | CVE-2021-35464 | ForgeRock AM 服务器 Java 反序列化漏洞               | ✔    |
| CVE（2021） | CVE-2021-35587 | Oracle Access Manager 身份验证绕过漏洞              | ✔    |
| CVE（2021） | CVE-2021-37538 | SmartDataSoft SmartBlog for PrestaShop SQL 注入漏洞 | ✔    |
| CVE（2021） | CVE-2021-37704 | PhpFastCache 信息泄露漏洞                           | ✔    |
| CVE（2021） | CVE-2021-39211 | GLPI 信息泄露漏洞                                   | ✔    |
| CVE（2021） | CVE-2021-39226 | Grafana 漏洞                                        | ✔    |
| CVE（2021） | CVE-2021-39327 | BulletProof Security WordPress信息泄露漏洞          | ✔    |
| CVE（2021） | CVE-2021-40149 | E1 Zoom信息泄露漏洞                                 | ✔    |
| CVE（2021） | CVE-2021-40859 | Auerswald COMpact 5500R后门漏洞                     | ✔    |
| CVE（2021） | CVE-2021-40875 | Gurock TestRail感信息泄露漏洞                       | ✔    |
| CVE（2021） | CVE-2021-41192 | Redash 伪造会话漏洞                                 | ✔    |
| CVE（2021） | CVE-2021-41266 | Minio身份验证绕过漏洞                               | ✔    |
| CVE（2021） | CVE-2021-41381 | Payara Micro Community目录遍历漏洞                  | ✔    |
| CVE（2021） | CVE-2021-41649 | PuneethReddyHC SQL注入漏洞                          | ✔    |
| CVE（2021） | CVE-2021-43496 | Clustering目录遍历漏洞                              | ✔    |
| CVE（2021） | CVE-2021-43798 | Grafana目录遍历漏洞                                 | ✔    |
| CVE（2021） | CVE-2021-44077 | Zoho远程代码执行漏洞                                | ✔    |
| CVE（2021） | CVE-2021-44152 | Reprise RLM越权漏洞                                 | ✔    |
| CVE（2021） | CVE-2021-44427 | Rosario 学生信息系统SQL 注入漏洞                    | ✔    |
| CVE（2021） | CVE-2021-44515 | Zoho远程代码执行漏洞                                | ✔    |
| CVE（2021） | CVE-2021-44529 | Ivanti EPM 云服务设备RCE漏洞                        | ✔    |
| CVE（2021） | CVE-2021-46381 | D-Link DAP-1620目录遍历漏洞                         | ✔    |
| CVE（2021） | CVE-2021-46417 | Franklin Fueling Systems Colibr信息泄露漏洞         | ✔    |
| CVE（2021） | CVE-2021-46422 | Telesquare SDT-CW3B1命令注入漏洞                    | ✔    |
| CVE（2020） | CVE-2020-12478 | eamPass 注入漏洞                                    | ✔    |
| CVE（2020） | CVE-2020-13700 | WordPress acf-to-rest-api 信息泄露漏洞              | ✔    |
| CVE（2020） | CVE-2020-13937 | Apache Kylin 安全漏洞                               |✔     |
| CVE（2020） | CVE-2020-14181 | Atlassian Jira 信息泄露漏洞                         |✔     |
| CVE（2020） | CVE-2020-14408 | Agentejo Cockpit 跨站脚本漏洞                       |✔     |
| CVE（2020） | CVE-2020-15148 | Yii 代码问题漏洞                                    |✔     |
| CVE（2020） | CVE-2020-35338 | Mobile Viewpoint Wireless Multiplex Terminal 信任管理问题漏洞|✔|
| CVE（2020） | CVE-2020-35476 | OpenTSDB 命令注入漏洞|✔|
| CVE（2020） | CVE-2020-35489 | Wordpress contact-form-7 代码问题漏洞|✔|
| CVE（2020） | CVE-2020-35736 | Liftoff GateOne 路径遍历漏洞|✔|
| CVE（2020） | CVE-2020-36112 | Projectworlds Online Book Store Project In Php SQL注入漏洞|✔|
| CVE（2020） | CVE-2020-36289 | Atlassian JIRA Server 和 Atlassian JIRA Data Center 信息泄露漏洞|✔|
| CVE（2020） | CVE-2020-26948 | Emby Server 代码问题漏洞|✔|
| CVE（2020） | CVE-2020-27361 | Akkadian Provisioning Manager 安全漏洞|✔|
| CVE（2020） | CVE-2020-27467 | Lfi-ProcessWire Cms  路径遍历漏洞|✔|
| CVE（2020） | CVE-2020-27866 | 多款Netgear产品授权问题漏洞|✔|
| CVE（2020） | CVE-2020-27982 | IceWarp Mail Server 跨站脚本漏洞|✔|
| CVE（2020） | CVE-2020-29395 | WordPress plugin 跨站脚本漏洞|✔|
| CVE（2020） | CVE-2020-24312 | WordPress plugin mndpsingh287 WP File Manager  信息泄露漏洞|✔|
| CVE（2020） | CVE-2020-24550 | Elastic EpiServer Find 输入验证错误漏洞|✔|
| CVE（2020） | CVE-2020-24571 | NexusQA NexusDB 路径遍历漏洞|✔|
| CVE（2020） | CVE-2020-24949 | PHP-Fusion 安全漏洞|✔|
| CVE（2020） | CVE-2020-26073 | Cisco?SD-WAN vManage 信息泄露漏洞|✔|
| CVE（2020） | CVE-2020-26876 | WordPress 安全漏洞|✔|
| CVE（2020） | CVE-2020-16139 | Cisco 7937G 输入验证错误漏洞|✔|
| CVE（2020） | CVE-2020-17453 | WSO2 Management Console 跨站脚本漏洞|✔|
| CVE（2020） | CVE-2020-17519 | Apache Flink 安全漏洞|✔|
| CVE（2020） | CVE-2020-19625 | sheila1227 gridx 安全漏洞|✔|
| CVE（2020） | CVE-2020-20300 | Weiphp SQL注入漏洞                       | ✔    |
| CVE（2020） | CVE-2020-23015 | Deciso OPNsense 输入验证错误漏洞          | ✔    |
| CVE（2019） | CVE-2019-0230  | Apache Struts远程代码执行漏洞             | ✔    |
| CVE（2019） | CVE-2019-2578  | Oracle 未授权访问漏洞                     | ✔    |
| CVE（2019） | CVE-2019-2588  | Oracle Fusion Middleware未授权访问漏洞    | ✔    |
| CVE（2019） | CVE-2019-3912  | LabKey Server Community Edition重定向漏洞 | ✔    |
| CVE（2019） | CVE-2019-6715  | WordPress 任意文件读取漏洞                | ✔    |
| CVE（2019） | CVE-2019-8449  | Jira 信息泄露漏洞                         | ✔    |
| CVE（2019） | CVE-2019-8903  | Total.js 平台路径遍历漏洞                 | ✔    |
| CVE（2019） | CVE-2019-10092 | Apache HTTP Server跨站点脚本问题          | ✔    |
| CVE（2019） | CVE-2019-10232 | Teclib GLPI SQL 注入漏洞                  | ✔    |
| CVE（2019） | CVE-2019-10717 | BlogEngine.NET 目录遍历漏洞               | ✔    |
| CVE（2019） | CVE-2019-11248 | Kubernetes healthz 端口公开               | ✔    |
| CVE（2019） | CVE-2019-11581 | Jira 模板注入漏洞                         | ✔    |
| CVE（2019） | CVE-2019-12583 | Zyxel UAG、USG 和 ZyWall设备未授权访问    | ✔    |
| CVE（2019） | CVE-2019-12962 | LiveZilla Server XSS漏洞                  | ✔    |
| CVE（2019） | CVE-2019-13101 | D-Link DIR-600M 信息泄露漏洞              | ✔    |
| CVE（2019） | CVE-2019-13462 | Lansweeper SQL 注入漏洞                   | ✔    |
| CVE（2019） | CVE-2019-14322 | Pallets Werkzeug 错误处理驱动器名称       | ✔    |
| CVE（2019） | CVE-2019-14974 | SugarCRM Enterprise XSS漏洞               | ✔    |
| CVE（2019） | CVE-2019-15858 | WordPress XSS漏洞                         | ✔    |
| CVE（2019） | CVE-2019-16313 | fw8 Router ROM 信息泄露漏洞               | ✔    |
| CVE（2019） | CVE-2019-16996 | Metinfo 7.0.0beta SQL 注入漏洞            | ✔    |
| CVE（2019） | CVE-2019-17382 | Zabbix 登录绕过漏洞                       | ✔    |
| CVE（2019） | CVE-2019-17418 | MetInfo SQL 注入漏洞                      | ✔    |
| CVE（2019） | CVE-2019-17503 | Kirona 动态资源调度 (DRS)信息泄露漏洞     | ✔    |
| CVE（2019） | CVE-2019-18393 | Ignite Realtime Openfire 目录遍历漏洞     | ✔    |
| CVE（2019） | CVE-2019-18922 | AT-S107 V.1.1.3 目录遍历漏洞              | ✔    |
| CVE（2019） | CVE-2019-19368 | Rumpus FTP Web XSS漏洞                    | ✔    |
| CVE（2019） | CVE-2019-19781 | Citrix ADC 和网关 目录遍历漏洞            | ✔    |
| CVE（2019） | CVE-2019-20085 | TVT NVMS-1000 设备 目录遍历漏洞           | ✔    |
| CVE（2019） | CVE-2019-20933 | InfluxDB 身份验证绕过漏洞                 | ✔    |
| 用友        |                | yongyou-ERP-NC-目录遍历漏洞               | ✔    |
| 用友        |                | yongyou-nc-RCE                            | ✔    |
| 用友        |                | yongyou-本地文件包含漏洞                  | ✔    |
| springboot  |                | springboot-actuators-jolokia-xxe漏洞      | ✔    |
| 致远        |                | 致远文件上传漏洞                          | ✔    |
| 致远        |                | 致远-oa-info-leak漏洞                     | ✔    |
| 锐捷        |                | 锐捷网关命令执行漏洞                      | ✔    |
| ThinkPHP    |                | thinkphp-509-information-disclosure       | ✔    |
| 通用        |                | 任意文件读取漏洞                          | ✔    |

POC将持续更新



# 问题反馈
首先感谢您花费时间来使scalpel变得更好用👍

如有任何误报需求等问题可以通过以下方式进行反馈

1、GitHub issue：https://github.com/StarCrossPortal/scalpel/issues

2、微信公众号：微信扫描以下二维码，关注我们

![公众号](picture/%E5%85%AC%E4%BC%97%E5%8F%B7.png)
# 相关资料
## KCON 2022

* https://mp.weixin.qq.com/s/MCtwiT93Fo9Js9ekuD-8wA
* https://mp.weixin.qq.com/s/hwpr1dmZX6RdAAM5OkgdfQ
