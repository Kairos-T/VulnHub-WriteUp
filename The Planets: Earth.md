Link: [The Planets: Earth](https://www.vulnhub.com/entry/the-planets-earth,755/)

[Walkthrough (Video) by Techno Science](https://youtu.be/e9de7AK0i2s):
Walkthrough (Text): 

### Enumeration
Interface name: `ifconfig`

Get target IP: `sudo netdiscover -i eth1` - Interface name

Network Scan for Open Ports: `nmap -sV -sC -v -T4 192.168.56.103 `
No. of open ports: 3 
2 Host names

`sudo nano /etc/hosts`
Paste host name with IP address
`192.168.56.193 earth.local terratest.earth.local`
CTRL+X+ENTER  
