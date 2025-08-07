Nmap 7.97SVN （ https://nmap.org ）

速查表,人工校验

用法：nmap [扫描类型] [选项] {目标规范}

目标说明：

```
可以传主机名、IP 地址、网络等。
例如：scanme.nmap.org，microsoft.com/24,192.168.0.1;10.0.0-255.1-254
-iL <inputfilename>： 从文件中读取主机/网络列表
-iR <num hosts>：选择随机目标
--exclude <host1[，host2][，host3],...>：排除某些主机/网络
--excludefile <exclude_file>：从文件中读取排除列表
```

主机发现：

```
-sL：List Scan列表扫描 - 简单地列出要扫描的目标
-sn：Ping 扫描 - 不进行端口扫描
-Pn：将所有主机都视为在线 -- 即跳过主机发现
-PS/PA/PU/PY[portlist]：对给定的端口使用 TCP SYN、TCP ACK、UDP 或 SCTP 发现
-PE/PP/PM：ICMP回显、时间戳和网络掩码请求发现探针
-PO[协议列表]：IP 协议 Ping
-n/-R：从不进行DNS解析/始终解析DNS [默认：sometimes]
--dns-servers <serv1[，serv2],...>：指定自定义 DNS 服务器
--system-dns：使用本系统的DNS解析器
--traceroute：跟踪到每个主机的跳路径
```

扫描技术：

```
-sS/sT/sA/sW/sM：TCP SYN / Connect（）/ ACK / Window / Maimon 扫描
-sU：UDP 扫描
-sN/sF/sX：TCP Null / FIN / Xmas 扫描
--scanflags <flags>：自定义 TCP 扫描标志
-sI <zombie host[:p robeport]>：空闲扫描
-sY/sZ：SCTP INIT/COOKIE-ECHO 扫描
-sO：IP 协议扫描
-b <FTP relay host中继主机>：FTP 反弹扫描
```

端口规格和扫描顺序：

```
-p <端口范围>：扫描指定端口
例如：-p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
--exclude-ports <端口范围>：从扫描中排除指定端口
-F：快速模式 - 扫描的端口比默认扫描少
-r：按顺序扫描端口 - 不要随机化
--top-ports <number>：扫描前<number>个最常见的端口
--port-ratio <ratio>：扫描比<ratio>更常见的端口
```

服务/版本检测：

```
-sV：探测打开的端口以确定服务/版本信息
--version-intensity <level>：设置版本扫描强度,从 0（轻量）到 9（尝试所有探测）
强度水平说明了应该使用哪些探测报文。数值越高， 服务越有可能被正确识别。
然而，高强度扫描花更多时间。强度值必须在0和9之间。
--version-light：轻量扫描,限制为最可能的探测（强度 2）
--version-all：尝试每个探测报文（强度 9）
--version-trace：显示详细的版本扫描活动（用于调试）
```

脚本扫描：

```
-sC：相当于 --script=default
--script=<Lua scripts>： <Lua scripts>是一个逗号分隔的列表目录、脚本文件或脚本类别
--script-args=<n1=v1，[n2=v2,...]>：为脚本提供参数
--script-args-file=filename：从文件中提取NSE脚本参数
--script-trace：显示所有发送和接收的数据
--script-updatedb：更新脚本数据库。
--script-help=<Lua scripts>：显示有关脚本的帮助。
<Lua scripts> 是一个以逗号分隔的脚本文件或script-categories列表 。
```

操作系统检测：

```
-O：启用系统检测
--osscan-limit：针对指定的目标进行操作系统检测
--osscan-guess：推测操作系统检测结果
```

时间和性能：

```
需要的选项<time>以秒为单位，或附加'ms'（毫秒）,'s'（秒）,'m'（分钟）或'h'（小时）到该值（例如 30m）。
-T<0-5>：设置时序模板（越高越快）
--min-hostgroup/max-hostgroup <size>：调整并行扫描组的大小
--min-parallelism/max-parallelism <numprobes>： 调整探测报文的并行度
--min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>：调整探测报文超时
--max-retries <tries>：限制端口扫描探针重新传输的次数。
--host-timeout <time>：放弃低速目标主机
--scan-delay/--max-scan-delay <time>： 调整探测报文之间的延迟
--min-rate <number>：发送数据包的速度不低于<number>每秒
--max-rate <number>：发送数据包的速度不超过<number>每秒
```

防火墙/IDS 规避和欺骗：

```
-f;--mtu <val>：分段数据包（可选，使用指定的MTU）
-D <decoy1，decoy2[，ME],...>：用诱饵隐藏扫描
-S <IP_Address>： 源地址欺骗
-e <iface>： 使用指定的接口
-g/--source-port <portnum>：使用给定的端口号,源端口欺骗
--proxies <url1，[url2],...>：通过 HTTP/SOCKS4 代理中继连接
--data <hex string>：将自定义有效负载附加到已发送的数据包
--data-string ：将<string>自定义 ASCII 字符串附加到发送的数据包中
--data-length <num>：将随机数据附加到发送的数据包中
--ip-options <options>：发送具有指定 ip 选项的数据包
--ttl <val>： 设置 IP 生存时间字段
--spoof-mac <mac 地址/前缀/供应商名称>：MAC地址欺骗
--badsum：发送带有虚假 TCP/UDP/SCTP 校验和的数据包
```

输出：

```
-oN/-oX/-oS/-oG <file>：正常、XML、s|<rIpt kIddi3输出扫描、和Grep输出格式,并分别设置为给定的文件名。
-oA <basename>： 一次输出三种主要格式
-v：增加详细程度（使用 -vv 或更多以获得更大的效果）
-d：提高调试级别（使用 -dd 或更高以获得更大的效果）
--reason：显示端口处于特定状态的原因
--open：仅显示打开（或可能打开）的端口
--packet-trace：显示所有发送和接收的数据包
--iflist：打印主机接口和路由（用于调试）
--append-output：附加到而不是破坏指定的输出文件
--resume <filename>：恢复中止的扫描
--noninteractive：通过键盘禁用运行时交互
--stylesheet <path/URL>：设置XSL样式表，转换XML输出
--webxml：参考 Nmap.Org 的样式表，以获得更可移植的 XML
--no-stylesheet：防止将XSL样式表与XML输出相关联,忽略XML声明的XSL样式表
```

杂项：

```
-6：启用 IPv6 扫描
-A：启用作系统检测、版本检测、脚本扫描和 traceroute
--datadir <dirname>：指定自定义 Nmap 数据文件位置
--send-eth/--send-ip：使用原始以太网帧或 IP 数据包发送
--privileged：假设用户具有完全特权
--unprivileged：假设用户缺乏原始套接字权限
-V：打印版本号
-h：打印此帮助摘要页。
```

例子：
```
nmap -v -A scanme.nmap.org
nmap -v -sn 192.168.0.0/16 10.0.0.0/8
nmap -v -iR 10000 -Pn -p 80
```

有关更多选项和示例，请参见手册页 （https://nmap.org/book/man.html）
