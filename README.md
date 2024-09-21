# cloudflare
Cloudflare白嫖大全，只提供大致操作及思路，具体操作请自行google
准备工作：
注册账号：https://dash.cloudflare.com/
域名注册：https://www.namesilo.com/

## cloudflare域名加速，内网穿透
1、进入首页，绑定添加域名，选择免费计划，继续
2、dns扫描完成之后，点击继续激活，然后按要求将为你分配的 Cloudflare 服务器在域名服务商那里添加到 NameServers
3、完成之后返回cloudflare首页域名就会变成激活状态（可能需要一定时间），cloudflare会为你免费抵挡ddos攻击，以及加速等
4、激活完成之后，如果你有固定公网ip即可在dns解析中添加解析，之后便可通过公网访问本地服务，如果是动态公网ip可使用dns-go等动态服务插件或其他动态服务商进行动态解析
5、如果没有公网ip，可进入首页，然后选择Zero Trust，进入Network，Tunnels创建隧道进行内网穿透，创建选择Cloudflared，然后按照指引安装软件，执行命令，完成隧道绑定

## cloudflare永久免费科学上网
1、进入首页，选择Wokers和Pages，创建works，随便取名，然后部署
2、进入刚才创建的works，点击编辑代码，https://raw.githubusercontent.com/zizifn/edgetunnel/main/src/worker-vless.js，复制里面的代码，粘贴，保存，部署
3、works点击进入设置，添加变量，第一个：UUID，此处生成：https://1024tools.com/uuid/，随便复制一个添加，第二个变量：PROXYIP，值：workers.cloudflare.cyou，也可使用优选IP工具筛选出的IP
4、变量添加完成后，便可在“域和路由”，复制路由地址后面加上你刚才添加的UUID，在浏览器访问，便会返回一个vless订阅地址，在v2ray中添加服务器，然后开启设置，Core:基础设置，修下面的分片设置，再修改添加的vless服务ip地址，可选
bestcf.onecf.eu.org
104.19.62.86
acsg3.cloudflarest.link
节点可选443端口，将节点地址换成优选域名，删除SNI；或者端口2082，关闭TLS。
443端口节点需启用分片。
也可使用优选IP，若网络不好，则可切换IP
5、优选IP，工具地址：https://github.com/XIU2/CloudflareSpeedTest/releases 或者 https://github.com/badafans/better-cloudflare-ip/releases，运行后可筛选出速度较好的IP地址，tips：优选IP的时候一定要先关闭代理

至此，已经可以科学上网，且可解锁Netflix，推荐平时看Youtube或者追剧的时候可以使用
本仓库已上传需要使用的工具软件
