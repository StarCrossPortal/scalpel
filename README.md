# scalpel🗡
scalpel是一款命令行扫描器，**它可以深度解析http请求中的参数，从而根据poc产生更加精确的http报文**。目前支持http被动代理模式进行扫描。用户可以自定义POC，同时我们也在Github上公开了POC仓库。
# 免责声明
本工具仅面向合法授权的企业安全建设行为，如您需要测试本工具的可用性，请自行搭建靶机环境。

为避免被恶意使用，本项目所有收录的poc均为漏洞的理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。

在使用本工具进行检测时，您应确保该行为符合当地的法律法规，并且已经取得了足够的授权。**请勿对非授权目标进行扫描**。

如您在使用本工具的过程中存在任何非法行为，您需自行承担相应后果，我们将不承担任何法律及连带责任。

在安装并使用本工具前，**请您务必审慎阅读、充分理解各条款内容，限制、免责条款或者其他涉及您重大权益的条款**可能会以加粗、加下划线等形式提示您重点注意。 除非您已充分阅读、完全理解并接受本协议所有条款，否则，请您不要安装并使用本工具。您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。
# 支持的POC列表
POC会不断进行更新，以支持检测更多的漏洞。
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

已支持漏洞检测列表

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
# scalpel下载
scalpel是单文件的二进制可执行文件，由纯go语言编写，无需安装其它依赖，下载之后可以直接使用。scalpel支持多个平台，请根据您的平台或者需求下载相应的版本。
* Windows X64

        scalpel-windows-amd64

* Windows X86

        scalpel-windows-x86
* Linux X64

        scalpel-linux-amd64

* Linux x86

        scalpel-linux-x86
* Linux ARM64

        scalpel-linux-arm64

* MacOS ARM64(适用于M1芯片的MacOS)

        scalpel-darwin-arm64
* MacOS X64(适用于Intel芯片的MacOS)

        scalpel-darwin-amd64

sha256.txt 是校验文件，内含个版本二进制文件的 sha256 的哈希值，请下载后自行校验以防被劫持。
# 用法
        Usage:
  scalpel [flags]
  scalpel [command]

Available Commands:
  genca       Generate ca certificate
  help        Help about any command
  poc         Poc mode, use poc to scan for vulnerabilities

Flags:
  -h, --help      help for scalpel
  -v, --version   version for scalpel

Use "scalpel [command] --help" for more information about a command.

# 运行
下载之后，进行解压，会产生两个文件，其中scalpel-xxx是对应平台的二进制可执行文件，而config.yaml是scalpel的配置文件，可以通过config.yaml对scalpel进行配置。
## Windows
在Window下，您可以在Windows的cmd或者powershell通过运行`.\scalpel-windows-amd64.exe -v`来运行scalpel，即可查看到scalpel的版本号。
## Linux
在Linux下，您可以在终端中通过运行`.\scalpel-linux-amd64 -v`来运行scalpel，即可查看到scalpel的版本号。如果您无法执行scalpel，可能是因为scalpel的二进制程序没有可执行权限，你可以通过`chmod +x scalpel-linux-amd64`命令来赋予scalpel可执行权限。
## MacOS
在MacOS下，您可以打开您使用的终端工具，比如 Terminal 或者 iTerm，然后在终端中通过运行`.\scalpel-linux-amd64 -v`来运行scalpel，即可查看到scalpel的版本号。
# 配置和使用
配置和使用详情请见[Wiki](https://github.com/StarCrossPortal/scalpel/wiki/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E6%89%AB%E6%8F%8F)
# POC编写说明
有关POC的编写，见[POC编写指南](https://github.com/StarCrossPortal/scalpel/wiki/POC%E7%BC%96%E5%86%99%E6%8C%87%E5%8D%97)
# 反馈及贡献POC
首先感谢您花费时间来使scalpel变得更好用👍

**Bug反馈**

请提交在GitHub Issues中，提供当前的scalpel版本、报错信息或截图、能够复现这个问题的环境并详细描述您的复现步骤。

**功能建议**

在GitHub Discussions中您可以畅所欲言，同开发人员讨论您想要的功能。

**POC贡献**

贡献者以 PR 的方式向 githuh 仓库内提交POC，在提交之前请搜索仓库的 poc 文件夹以及 Github 的 Pull request, 确保该 POC 没有被提交。
# 讨论区
如有问题可以在 星阑实验室公众号反馈

微信公众号：微信扫描以下二维码，关注我们

![公众号](picture/%E5%85%AC%E4%BC%97%E5%8F%B7.png)
# 相关资料
## KCON 2022

* https://mp.weixin.qq.com/s/hwpr1dmZX6RdAAM5OkgdfQ
