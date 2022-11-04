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
POC是以yaml文件的形式来进行编写。下面是POC可以包含的所有内容。您可以根据需要，选择其中某些部分来使用。下面是对POC文件中字段的一些解释。下面的内容保存在github的poc-rule.yaml文件中。
```yaml
info:                                 # 基本信息部分POC的编写者可以任意进行修改。
  author: test                        # 编写者
  name: test                          # 规则名称
  description: test                   # 规则描述
  time: 2022/10/20                    # 编写（修改）时间
  note: test                          # 备注信息
  reference:                          # 相关信息
    - test

mutate_rule:                          # 数组值，可以有多组，它们之间是And关系。
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    header_all: false                 # 布尔值，表示是否对http的所有header进行变异。
    header_filter:                    # 数组值，可以通过参数名称或者参数值筛选你想要变异的http header，
    - 
      args:                           # 整数，只能取1或2，分别表示参数名称，参数值。
      operator:                       # 整数，只能取1或2，分别表示正则匹配，字符串相等
      value:                          # 字符串，你想筛选的值
    body_all_leaf_argname: false      # 布尔值，表示是否对body中所有叶子结点的参数名进行变异
    body_all_leaf_argvalue: false     # 布尔值，表示是否对body中所有叶子结点的参数值进行变异
    body_leaf_add_node:               # 数组值，表示body新增叶子节点
    - 
      argname:                        # 字符串，表示参数名
      argvalue:                       # 字符串，表示参数值
    body_root_add_node:               # 数组值，表示在body的根节点下面直接新增子节点
    - 
      argname:                        # 字符串，表示参数名
      argvalue:                       # 字符串，表示参数值
    body_filter:                      # 数组值，可以通过参数名称或者参数值筛选你想要变异的body节点
    - 
      args:                           # 整数，只能取1或2，分别表示参数名称，参数值。
      operator:                       # 整数，只能取1或2，分别表示正则匹配，字符串相等
      value:                          # 字符串，你想筛选的值
    body_str: false                   # 布尔值，表示是否对body字符串整体进行操作
    method: false                     # 布尔值，表示是否对method进行操作
    netloc: false                     # 布尔值，表示是否对url中网络位置部分进行操作
    path: false                       # 布尔值，表示是否对进行操作
    query_str:                        # 布尔值，表示是否对query整体进行操作
    url:                              # 布尔值，表示是否对整个url进行操作，指的是HTTP报文中不含有协议和域名的URL
    query_leaf_argname:               # 布尔值，表示是否对所有的query参数名进行操作
    query_leaf_argvalue:              # 布尔值，表示是否对所有的query参数值进行操作
    query_add_node:                   # 数组值，表示query新增的子节点
    - 
      argname:                        # 字符串，表示参数名
      argvalue:                       # 字符串，表示参数值
    query_filter:                     # 数组值，可以通过参数名称或者参数值筛选你想要变异的query节点
    - 
      args:                           # 整数，只能取1或2，分别表示参数名称，参数值。
      operator:                       # 整数，只能取1或2，分别表示正则匹配，字符串相等
      value:                          # 字符串，你想筛选的值
  
  mutate_way:                         # 数组值，变异方式。表示对你选择的变异位置进行变异的方式，可以有多组，它们之间是OR关系
  - 
    pos:                              # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value:                            # 字符串，表示你想要的值

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-                                     # 每组内的参数之间是AND关系
  status_code:                        # 表示响应状态码
    value:                            # 需要检查的状态码的值
    operator:                         # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于
  resp_headers:                       # 表示响应中的headers
    value:                            # 需要检查的响应头中的值
    operator:                         # 比较规则，可以取值1，2;；分别代表操作是字符串包含，正则匹配
  resp_body:                          # 表示响应中的body
    value:                            # 需要检查的响应体中的值
    operator:                         # 比较规则，可以取值1，2；分别代表操作是字符串包含，正则匹配
```
需要注意的是，response_check部分是用来编写响应检查的，这部分编写的好坏与否会影响到扫描结果的准确率。下面通过一些例子来直观的展示如何编写POC。一个HTTP报文如下所示：

	POST /post HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate, br
	Connection: keep-alive
	Content-Length: 45
	Content-Type: application/json
	User-Agent: python-httpx/0.22.0

	{"userinfo": {"name": "jack", "age": 22}}
## poc示例1
如果需要将path从/post更改为/index.html，那么编写的POC如下所示，这里省略了poc文件中的info部分。
```yaml
mutate_rule:
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    url: true                         # 对URL进行变异
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: /index.html

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-
  status_code:                        # 表示响应状态码
    value: 200                        # 需要检查的状态码的值
    operator: 1                       # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于
```
这个poc表示的含义就是更改路径/post为/index.html；响应的检查规则是响应状态码的值等于200
## poc示例2
如果需要将请求体中的参数name的值改为"wang"，那么编写的POC如下所示，同样，这里省略了poc文件中的info部分。
```yaml
mutate_rule:                          # 数组值，可以有多组，它们之间是And关系。
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    body_all_leaf_argvalue: true      # 布尔值，表示是否对body中所有叶子结点的参数值进行变异
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: wang

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-                                     # 每组内的参数之间是AND关系
  status_code:                        # 表示响应状态码
    value: 200                        # 需要检查的状态码的值
    operator: 5                       # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于。其中大于，小于，等于只适用于数值
```
这样，就会产生如下所示的两个报文。

	POST /post HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate, br
	Connection: keep-alive
	Content-Type: application/json
	User-Agent: python-httpx/0.22.0

	{"userinfo": {"name": "zhangsan", "age": "wang"}}


	POST /post HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate, br
	Connection: keep-alive
	Content-Type: application/json
	User-Agent: python-httpx/0.22.0

	{"userinfo": {"name": "wang", "age": 10}}
其中第二个报文就是我们想要的，它会将name的值替换为wang。至于为什么要产生第一个报文，这是因为我们这里提供的方式是变异全部的叶子节点。这样能够达到一定程度上fuzz的意义。会使的poc在一定程度上智能化，而不是固定某种模式下的poc。这也是为什么提供了随机插入以及尾部插入的原因。另外一个可能性，例如想替换用户名相关的参数，但是关键的字段可能叫username, user_name, UserName, UName, user, name等。当你无法确定字段名称的时候，这种你就需要这样的Fuzz可能性。
## poc示例3
可能绝大多数的场景都是相对固定的POC，比如大多数的CVE漏洞的POC都是相对固定位置的变化。因此，该示例将展示对整个body进行替换的操作。
```yaml
mutate_rule:                          # 数组值，可以有多组，它们之间是And关系。
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    body_str: true                    # 布尔值，表示是否对body字符串整体进行操作
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: '{"user":admin, "pass":"123456"}'

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-                                     # 每组内的参数之间是AND关系
  status_code:                        # 表示响应状态码
    value: 200                        # 需要检查的状态码的值
    operator: 5                       # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于。其中大于，小于，等于只适用于数值
```
这样的POC，对于上面的请求而言，将会产生如下的变异结果。

	POST /post HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate, br
	Connection: keep-alive
	Content-Type: application/json
	User-Agent: python-httpx/0.22.0

	{"user":admin, "pass":"123456"}
## poc示例4
你也可以选择共同改变其中的某些选项，例如，将上面的Content-Type替换为application/x-www-form-urlencoded，将body替换为user=admin&pass=admin
```yaml
mutate_rule:                          # 数组值，可以有多组，它们之间是And关系。
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    body_str: true                    # 布尔值，表示是否对body字符串整体进行操作
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: user=admin&pass=admin
-
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    header_all: true                    # 布尔值，表示是否对所有的header进行操作
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: application/x-www-form-urlencoded

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-                                     # 每组内的参数之间是AND关系
  status_code:                        # 表示响应状态码
    value: 200                        # 需要检查的状态码的值
    operator: 5                       # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于。其中大于，小于，等于只适用于数值
```
这样的POC将会产生很多的报文，而下面这个报文就是我们需要的。

	POST /post HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate, br
	Connection: keep-alive
	Content-Type: application/x-www-form-urlencoded
	User-Agent: python-httpx/0.22.0

	user=admin&pass=admin
暂时没有提供指定某个参数进行变异的操作，这是因为想保留scalpel的Fuzz特性，而非单纯的相对固定位置的变异。
## poc示例5
这个示例将展示scalpel的Fuzz能力，例如：
```yaml
mutate_rule:                          # 数组值，可以有多组，它们之间是And关系。
- 
  mutate_position:                    # 变异位置，表示你选择哪些位置进行变异
    body_all_leaf_argvalue: true      # 布尔值，表示是否对body中所有叶子节点的参数值进行变异
  
  mutate_way:                         # 变异方式。表示对你选择的变异位置进行变异的方式
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: "aaaaa"
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: "aaaaaaaaaaaa"
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: "aaaaaaaaaaaaaaaaaaa"
  - 
    pos: 3                            # 整数，只能取1，2，3其中一个，分别表示插入末尾，插入随机位置以及替换
    value: "aaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
  - 

response_check:                       # 数组值，输出检查，用来检查poc是否命中，多个组之间是OR关系
-                                     # 每组内的参数之间是AND关系
  status_code:                        # 表示响应状态码
    value: 500                        # 需要检查的状态码的值
    operator: 5                       # 比较规则，可以取值1，2，3，4，5；分别代表操作是字符串包含，正则匹配，大于，小于以及等于。其中大于，小于，等于只适用于数值
```
这个poc展示的情形通常在测试边界值的时候是非常有用的，例如name字段，可能只允许长度是32以内的字符串，它能够帮助你测试出，超长的字符串可能引发的500问题。
## 贡献POC
贡献者以 PR 的方式向 githuh 仓库内提交POC，在提交之前请搜索仓库的 poc 文件夹以及 Github 的 Pull request, 确保该 POC 没有被提交。
# 相关资料
## KCON 2022

* https://mp.weixin.qq.com/s/hwpr1dmZX6RdAAM5OkgdfQ

# 讨论区
如有问题可以在 星阑实验室公众号反馈

微信公众号：微信扫描以下二维码，关注我们

![公众号](picture/%E5%85%AC%E4%BC%97%E5%8F%B7.png)