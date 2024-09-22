# cloudflare

Cloudflare白嫖大全，只提供大致操作及思路，具体操作请自行google

准备工作：

注册账号：https://dash.cloudflare.com/

域名注册：https://www.namesilo.com/


## 使用工具或地址

[v2ray](https://github.com/233boy/v2ray/tags)  [v2rayN](https://github.com/2dust/v2rayN/tags)

优选工具：[地址1](https://github.com/XIU2/CloudflareSpeedTest/releases)  [地址2](https://github.com/badafans/better-cloudflare-ip/releases) 


## cloudflare域名加速，内网穿透

1、进入首页，绑定添加域名，选择免费计划，继续

2、dns扫描完成之后，点击继续激活，然后按要求将为你分配的 Cloudflare 服务器在域名服务商那里添加到 NameServers

3、完成之后返回cloudflare首页域名就会变成激活状态（可能需要一定时间），cloudflare会为你免费抵挡ddos攻击，以及加速等

4、激活完成之后，如果你有固定公网ip即可在dns解析中添加解析，之后便可通过公网访问本地服务，如果是动态公网ip可使用dns-go等动态服务插件或其他动态服务商进行动态解析

5、如果没有公网ip，可进入首页，然后选择Zero Trust，进入Network，Tunnels创建隧道进行内网穿透，创建选择Cloudflared，然后按照指引安装软件，执行命令，完成隧道绑定


## cloudflare永久免费科学上网

1、进入首页，选择Wokers和Pages，创建works，随便取名，然后部署

2、进入刚才创建的works，点击编辑代码，复制里面的[代码](https://raw.githubusercontent.com/zizifn/edgetunnel/main/src/worker-vless.js)，粘贴，保存，部署

3、works点击进入设置，添加变量，第一个：UUID，[此处生成](https://1024tools.com/uuid/)，随便复制一个添加，第二个变量：PROXYIP，值：workers.cloudflare.cyou，也可使用优选IP工具筛选出的IP

4、变量添加完成后，便可在“域和路由”，复制路由地址后面加上你刚才添加的UUID，在浏览器访问，便会返回一个vless订阅地址，在v2ray中添加服务器，然后开启设置，Core:基础设置，修下面的分片设置，再修改添加的vless服务ip地址，可选

bestcf.onecf.eu.org

104.19.62.86

acsg3.cloudflarest.link

节点可选443端口，将节点地址换成优选域名，删除SNI；或者端口2082，关闭TLS。

443端口节点需启用分片。

也可使用优选IP，若网络不好，则可切换IP

5、优选IP，下载优选工具，运行后可筛选出速度较好的IP地址，tips：优选IP的时候一定要先关闭代理


至此，已经可以科学上网，且可解锁Netflix，推荐平时看Youtube或者追剧的时候可以使用

## 自建订阅转换

原文：https://github.com/bulianglin/psub

原理：订阅转换服务器还是使用别人提供的，只是在转换之前先走一遍自建的cloudflare服务，将服务器地址，账户密码等全部随机修改为假数据，在订阅服务器转换完成之后在修改回来，此方法可减小订阅泄露风险

遇到问题：使用别人订阅转换服务时，可能会遇到526，SSL 协议无效，这是因为订阅转换的服务器地址没有有效的SSL证书，切换订阅转换服务器即可

1、进入cloudflare，创建works，部署

2、进入works，编辑代码：复制[代码](https://github.com/silvermoon89/psub/blob/main/worker.js)，粘贴，保存，部署

3、works设置变量，BACKEND，此变量即为订阅转换的服务器，下面提供一些，有的可能不支持vless，hysteria协议转换，这个是后端服务决定的，可以找支持的后端服务

https://sub.id9.cc 品云提供

https://sub.xeton.dev subconventer作者提供

https://api.dler.io  lhie1提供

4、添加KV命名空间，名称随意，然后绑定KV命名空间，变量名为SUB_BUCKET，此时便可使用路由中的地址访问订阅转换页面

##### 其他可选配置：

5、绑定自己域名，使用域名访问订阅转换页面

如果你有自己的域名且已经在cloudflare激活，你就可以在works中添加一个新的路由，例如sub.example.top/*，之后再cloudflare域名管理中设置dns解析，将你设置的子域名随便解析到一个dns，例如8.8.8.8，此时你就可以使用当前子域名访问订阅转换页面

6、选择自定义订阅转换规则

再前面的works代码中，有一个变量：const frontendUrl = 'https://raw.githubusercontent.com/bulianglin/psub/main/frontend.html'; 这里便是前端页面地址，你可以将文件上传到自己github仓库，找到label:"universal"，再这里添加自己的订阅转换文件地址，便可使用自定义策略及规则，当然你也可以直接复制地址在web页面粘贴使用

