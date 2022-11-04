# scalpel介绍
scalpel是一款命令行扫描器，**它可以深度解析http请求中的参数，从而根据poc产生更加精确的http报文**。目前支持http被动代理模式进行扫描。用户可以自定义POC，同时我们也在Github上公开了POC仓库。
# 免责声明
本工具仅面向合法授权的企业安全建设行为，如您需要测试本工具的可用性，请自行搭建靶机环境。

为避免被恶意使用，本项目所有收录的poc均为漏洞的理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。

在使用本工具进行检测时，您应确保该行为符合当地的法律法规，并且已经取得了足够的授权。**请勿对非授权目标进行扫描**。

如您在使用本工具的过程中存在任何非法行为，您需自行承担相应后果，我们将不承担任何法律及连带责任。

在安装并使用本工具前，**请您务必审慎阅读、充分理解各条款内容，限制、免责条款或者其他涉及您重大权益的条款**可能会以加粗、加下划线等形式提示您重点注意。 除非您已充分阅读、完全理解并接受本协议所有条款，否则，请您不要安装并使用本工具。您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。
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
# 运行
下载之后，进行解压，会产生两个文件，其中scalpel-xxx是对应平台的二进制可执行文件，而config.yaml是scalpel的配置文件，可以通过config.yaml对scalpel进行配置。
## Windows
在Window下，您可以在Windows的cmd或者powershell通过运行`.\scalpel-windows-amd64.exe -v`来运行scalpel，即可查看到scalpel的版本号。
## Linux
在Linux下，您可以在终端中通过运行`.\scalpel-linux-amd64 -v`来运行scalpel，即可查看到scalpel的版本号。如果您无法执行scalpel，可能是因为scalpel的二进制程序没有可执行权限，你可以通过`chmod +x scalpel-linux-amd64`命令来赋予scalpel可执行权限。
## MacOS
在MacOS下，您可以打开您使用的终端工具，比如 Terminal 或者 iTerm，然后在终端中通过运行`.\scalpel-linux-amd64 -v`来运行scalpel，即可查看到scalpel的版本号。
# 代理模式扫描
## 原理介绍
在scalpel的代理模式下，扫描器是作为中间人存在的，首先scalpel会原样转发您的流量，并返回服务器响应给客户端。同时scalpel会记录该流量，然后根据poc修改参数并重新发送请求进行扫描。这就是scalpel的基本原理。
## 生成CA证书
当客户端和服务器使用https协议进行通信的时候，scalpel作为中间人必须要得到客户端的信任，才能建立与客户端的通信。因此scalpel需要通过自定义的CA证书签发伪造的服务器证书，从而使客户端信任scalpel。这样scalpel才能和客户端建立连接，从而获取到流量内容。scalpel提供了genca命令来方便生成CA证书。
* Windows

        ./scalpel-windows-amd64 genca
* Linux

        ./scalpel-linux-amd64 genca
* MacOS

        ./scalpel-drawin-amd64 genca

运行命令之后，将在当前文件夹生成 ca.crt 和 ca.key 两个文件。genca命令只需要第一次使用的时候运行即可，如果文件已经存在再次运行会报错，需要先删除本地的 ca.crt 和 ca.key 文件。
## 安装CA证书
我们推荐将ca证书安装在操作系统上。当然您也可以根据不同的浏览器客户端自行进行ca证书的设置。下面是在不同的操作系统上进行安装的教程。如果您使用的是 FireFox 浏览器，请参照[https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)进行配置。
* Linux

    将生成的ca.crt文件复制到/usr/local/share/ca-certificates/目录下，然后执行update-ca-certificates命令即可。注意，这需要超级管理员权限。以Debian系列为例。

        sudo cp ca.crt /usr/local/share/ca-certificates/scalpel.crt
        sudo update-ca-certificates
* Windows
	
	在Windows下安装ca证书比较简单，双击ca.crt即可弹出安装证书的窗口，按照提示一步一步进行即可安装成功。
    
* MacOS

    在finder(访达)里打开ca.crt文件所在的目录，点击ca.crt即可进入到钥匙串访问页面。如下所示：
    ![钥匙串](picture/macos/%E7%82%B9%E5%87%BBca%E5%90%8E.jpg)
    点击左侧的登录菜单，将要安装的证书拖入到右侧证书列表的空白区域。刚拖入的证书logo右下角会有个❌，如下所示：
    ![导入证书](picture/macos/%E6%8B%96%E5%85%A5ca.jpg)
    右键点击证书，然后进入“显示简介”弹窗，点击信任折叠列表，设置使用此证书时 为“始终信任”。
    ![展开信任折叠列表](picture/macos/%E4%BF%A1%E4%BB%BBca.jpg)
    ![信任证书](picture/macos/%E6%9B%B4%E6%94%B9%E4%BF%A1%E4%BB%BB.jpg)
    然后在关闭“显示简介”弹窗时会要求输入电脑登录密码，输入密码即可。至此，CA证书安装完毕。安装成功的CA证书会在证书logo右下角出现➕。如下所示：
    ![安装成功](picture/macos/%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F.jpg)

## 配置代理
当安装完ca证书以后，就需要配置代理。通常大多数浏览器的设置功能中都提供了配置代理的功能。以Firefox浏览器为例，使用系统代理即可。
![浏览器配置代理](picture/%E6%B5%8F%E8%A7%88%E5%99%A8%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%90%86.png)

## 启动代理
在安装完ca证书和配置好代理以后，就可以使用被动扫描模式进行扫描了。例如：

    ./scalpel-linux-amd64 poc -l 127.0.0.1:8000 -f poc/test1.yaml -o 1.html
poc命令的参数如下所示：
|标志|含义|
|:--|:--|
|d|指定poc目录进行扫描，可以是多级目录|
|f|指定poc文件进行扫描，可以指定多个文件|
|l|指定监听的地址|
|o|指定扫描结果的输出文件|

需要注意的是，使用的时候必须要指定-o标志来指定扫描结果输出的html文档。

scalpel本身支持的每个交互都将包含在命令中。命令可以有子命令，并且可以选择运行操作。因此，你可以使用如下的命令来查看命令行帮助。

    ./scalpel-linux-amd64 poc -h
![poc命令帮助](picture/poc%E5%91%BD%E4%BB%A4%E5%B8%AE%E5%8A%A9.png)

当然了，在启动代理模式之前，你可以根据你的需要对配置文件就行配置。目前支持比较简单的一些配置，具体见配置文件config.yaml，后续可能会开放更多的配置。启动代理以后，就可以在浏览器中开始访问你想要测试网站了，如果发现漏洞，scalpel会在命令行有相关请求信息的输出。当你扫描完毕的时候，可以使用ctrl+c结束scalpel即可，如果有扫描结果，那么就会生成指定的html文件。否则不生成。
# 配置文件
下载的压缩包解压之后，会有一个config.yaml文件，此文件是scalpel的配置文件。可以根据您的环境进行具体的配置。
```yaml
# 全局 http 发包配置
http:
  proxy:                                # 漏洞扫描时使用的代理，如: http://127.0.0.1:8080
  read_timeout: 10                      # 等待 http 响应的超时时间，单位秒，默认10秒
  max_conns_per_host: 30                # 同一 host 最大允许的连接数，可以根据目标主机性能适当增大
  fail_retries: 0                       # 请求失败的重试次数，0 则不重试
  max_redirect: 0                       # 单个请求最大允许的重定向次数
  max_resp_body_size: 2097152           # 最大允许的响应大小, 单位byte，默认2Mb
  max_qps: 300                          # 每秒最大请求数

# 被动代理配置
mitm:
  ca_cert: ./ca.crt                     # CA 根证书路径
  ca_key: ./ca.key                      # CA 私钥路径
  restriction:                          # 代理能够访问的资源限制, 以下各项为空表示不限制
    hostname_allowed: []                # 允许访问的 Hostname，支持格式如 t.com、*.t.com
    hostname_disallowed:                # 不允许访问的 Hostname，支持格式如 t.com、*.t.com
    - '*google*'
    - '*baidu*'
    - '*.gov.cn'
    - '*.edu.cn'
    port_allowed: []                    # 允许访问的端口, 支持的格式如: 80、80-85
    port_disallowed: []                 # 不允许访问的端口, 支持的格式如: 80、80-85
    path_allowed: []                    # 允许访问的路径，支持的格式如: test、*test*
    path_disallowed: []                 # 不允许访问的路径, 支持的格式如: test、*test*
  queue_max_length: 3000                # 队列长度限制, 也可以理解为最大允许多少等待扫描的请求, 请根据内存大小自行调整
```
注意，队列长度的大小需要根据您的机器内存来进行调整，默认是3000，一般情况下都是可以的。
# POC编写说明
有关POC的编写，见[POC编写指南](https://github.com/StarCrossPortal/scalpel/wiki/POC%E7%BC%96%E5%86%99%E6%8C%87%E5%8D%97)
## 贡献POC
贡献者以 PR 的方式向 githuh 仓库内提交POC，在提交之前请搜索仓库的 poc 文件夹以及 Github 的 Pull request, 确保该 POC 没有被提交。
# 相关资料
## KCON 2022

* https://mp.weixin.qq.com/s/hwpr1dmZX6RdAAM5OkgdfQ

# 讨论区
如有问题可以在 星阑实验室公众号反馈

微信公众号：微信扫描以下二维码，关注我们

![公众号](picture/%E5%85%AC%E4%BC%97%E5%8F%B7.png)
