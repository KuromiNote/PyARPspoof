> # **PyARPspoof工具**
> **该工具仅用于测试、学习，请勿使用于违法用途，否则责任由使用者自行承担**

PyARPspoof项目可以自定义地发送ARP数据包给一定网络范围的目标主机应答，从而达到修改目标主机的ARP缓存表的目的

> ### 依赖

该项目引用了第三方库[Scapy](https://scapy.net/)，此第三方库在此是必要的

> ### Usage

```
 ██▓███ ▓██   ██▓ ▄▄▄       ██▀███   ██▓███    ██████  ██▓███   ▒█████   ▒█████    █████▒
▓██░  ██▒▒██  ██▒▒████▄    ▓██ ▒ ██▒▓██░  ██▒▒██    ▒ ▓██░  ██▒▒██▒  ██▒▒██▒  ██▒▓██   ▒ 
▓██░ ██▓▒ ▒██ ██░▒██  ▀█▄  ▓██ ░▄█ ▒▓██░ ██▓▒░ ▓██▄   ▓██░ ██▓▒▒██░  ██▒▒██░  ██▒▒████ ░ 
▒██▄█▓▒ ▒ ░ ▐██▓░░██▄▄▄▄██ ▒██▀▀█▄  ▒██▄█▓▒ ▒  ▒   ██▒▒██▄█▓▒ ▒▒██   ██░▒██   ██░░▓█▒  ░ 
▒██▒ ░  ░ ░ ██▒▓░ ▓█   ▓██▒░██▓ ▒██▒▒██▒ ░  ░▒██████▒▒▒██▒ ░  ░░ ████▓▒░░ ████▓▒░░▒█░    
▒▓▒░ ░  ░  ██▒▒▒  ▒▒   ▓▒█░░ ▒▓ ░▒▓░▒▓▒░ ░  ░▒ ▒▓▒ ▒ ░▒▓▒░ ░  ░░ ▒░▒░▒░ ░ ▒░▒░▒░  ▒ ░    
░▒ ░     ▓██ ░▒░   ▒   ▒▒ ░  ░▒ ░ ▒░░▒ ░     ░ ░▒  ░ ░░▒ ░       ░ ▒ ▒░   ░ ▒ ▒░  ░      
░░       ▒ ▒ ░░    ░   ▒     ░░   ░ ░░       ░  ░  ░  ░░       ░ ░ ░ ▒  ░ ░ ░ ▒   ░ ░    
         ░ ░           ░  ░   ░                    ░               ░ ░      ░ ░          
         ░ ░                                                                             
```

Usage: pyarpspoof to <1p ipv4 address> <2p ipv4 address> is [\<mac address\>/\<ipv4 address\>/me/fakemac]

这是一个ARP投毒(欺骗)攻击程序，它可以使目标的ARP缓存表变成你设定的内容。

使目标的网络通讯变得不正常，甚至可以作为中间人监听目标与另一个目标的数据包流量。

\<1p ipv4 address\>&emsp;&emsp;&ensp;指投毒目标

\<2p ipv4 address\>&emsp;&emsp;&ensp;指欺骗内容的IP地址

\<mac address\>&emsp;&emsp;&emsp;&emsp;指欺骗内容的MAC地址

\<ipv4 address\>&emsp;&emsp;&emsp;&emsp;指第三者的IP地址，会自动转化为MAC地址

\<me\>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;指本地主机MAC地址，通常作为中间人攻击，为关键词

\<fakemac\>&emsp;&emsp;&emsp;&emsp;&emsp;&ensp;&nbsp;指随机的虚假MAC地址，通常用于断网攻击，为关键词

了解ARP协议:

    ARP协议是根据IP地址获取物理地址（MAC地址）的TCP/IP协议。
    
    主机在向局域网内广播携带IP地址的ARP请求，然后更新ARP路由表，确保主机内主机IP地址和MAC地址的映射
    
了解ARP投毒(欺骗)攻击:

    攻击者向目标伪造ARP协议包，使得目标取得错误的ARP缓存。
    
    可以理解为，攻击者甲欺骗快递公司说“受害者乙的住址为XX:XX:XX:XX:XX:XX”，但是这里的住址其实是错误的，攻击者可以将地址设置为自己的住址，这样攻击者甲就能收到本该属于受害者乙的快递，攻击者可以查看、保存、修改、丢弃受害者乙的包裹
    
例如:

    pyarpspoof to 192.168.1.1 192.168.1.2 is me
    
    => 欺骗192.168.1.1，192.168.1.2的MAC地址是我的MAC地址(欺骗192.168.1.1自己是192.168.1.2)
    
    pyarpspoof to 192.168.1.2 192.168.1.1 is me
    
    => 欺骗192.168.1.2，192.168.1.1的MAC地址是我的MAC地址(欺骗192.168.1.2自己是192.168.1.1)
    
    pyarpspoof to 192.168.1.1 192.168.1.2 is 0A:48:71:CD:F8:A1
    
    => 欺骗192.168.1.1，192.168.1.2的MAC地址是0A:48:71:CD:F8:A1(欺骗192.168.1.1，192.168.1.1搬到了xx住址)
    
    pyarpspoof to 192.168.1.1 192.168.1.2 is fakemac
    
    => 欺骗192.168.1.1，192.168.1.2的MAC地址是随机MAC地址(欺骗192.168.1.1，192.168.1.2搬到了未知地址)
    

pyarpspoof help   获取帮助
